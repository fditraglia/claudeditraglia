# Zoom Meeting Summary

*v1.0 — Transcribe a Zoom recording and summarize it into meeting notes*

Transcribes a Zoom meeting recording using local whisper.cpp, then summarizes the transcript into structured meeting notes with key discussion points, decisions, action items, and open questions.

## Arguments

`$ARGUMENTS` can include:
- *(none)* — show a numbered list of recent Zoom recordings and ask which to transcribe
- `<number>` — select the Nth most recent Zoom recording from `~/Documents/Zoom/`

## Instructions

### Step 1: Select a recording

List recent Zoom recordings:

```bash
ls -1t ~/Documents/Zoom/ | head -15 | nl -ba
```

If `$ARGUMENTS` is a number, use it to select from the list. Otherwise, use AskUserQuestion to let the user pick (show the list as option descriptions, use meeting names as labels — present up to 4 most recent, with "Other" for older recordings).

Store the full path to the selected Zoom folder.

### Step 2: Convert audio

Find the `.m4a` file in the selected Zoom folder and convert to 16kHz mono WAV (what whisper expects):

```bash
ffmpeg -i "<path-to-m4a>" -ar 16000 -ac 1 -c:a pcm_s16le \
  -af "areverse,silenceremove=start_periods=1:start_silence=5:start_threshold=-40dB,areverse" \
  "/tmp/zoom-audio.wav" -y
```

The `silenceremove` filter trims trailing silence to prevent whisper from hallucinating repeated phrases on silent audio.

### Step 3: Transcribe

Check the audio duration first:

```bash
ffprobe -i "/tmp/zoom-audio.wav" -show_entries format=duration -v quiet -of csv="p=0"
```

Tell the user the estimated transcription time (roughly: duration in minutes / 15).

Run whisper-cli with the large-v2 model, VAD enabled, and max-context 0:

```bash
~/whisper.cpp/build/bin/whisper-cli \
  -m ~/whisper.cpp/models/ggml-large-v2.bin \
  -f /tmp/zoom-audio.wav \
  -np \
  -mc 0 \
  --vad \
  --vad-model ~/whisper.cpp/models/for-tests-silero-v6.2.0-ggml.bin \
  -otxt \
  -of "<zoom-folder>/transcript"
```

Key flags:
- **large-v2** (not v3) — v3 is prone to hallucination loops on long audio
- **`-mc 0`** — disables previous-text context, breaking the feedback loop that causes hallucination
- **`--vad`** — Voice Activity Detection skips silence, preventing hallucination on quiet segments

This saves `transcript.txt` in the Zoom recording folder alongside the audio.

Use a timeout of 600000ms (10 minutes) for the transcription command.

### Step 4: Summarize

Read the transcript and produce a structured meeting summary containing:

1. **Key discussion points** — the main topics and ideas discussed
2. **Decisions made** — anything that was agreed upon
3. **Action items / next steps** — concrete tasks arising from the meeting
4. **Open questions** — unresolved issues raised during the meeting

Use your understanding of the current project's context (read CLAUDE.md if available) to make the summary precise and domain-appropriate. Keep the tone concise and factual.

**Important**: The transcript does not identify speakers. Do NOT guess or attribute statements to specific people in the discussion points. For action items, use placeholder names like "TBD" and ask the user to assign them during review.

### Step 5: Append to meeting notes

Look for a meeting notes file in the current project:
1. `notes/meeting-notes.md`
2. `meeting-notes.md`

If found, insert the summary as a new `## Meeting <date>` section **immediately after the first top-level heading** (reverse chronological order — newest at top). Extract the meeting date from the Zoom folder name (format: `M/D/YYYY`).

If no meeting notes file exists, create `notes/meeting-notes.md` with a `# Meeting Notes` heading and the new entry.

### Step 6: Clean up

Remove the temporary WAV file:

```bash
rm /tmp/zoom-audio.wav
```

Report to the user:
- Where the full transcript was saved (the Zoom folder)
- Where the summary was written (the meeting notes file)
- Suggest they review and edit the summary

## Dependencies

- **whisper.cpp** — `~/whisper.cpp/build/bin/whisper-cli` with `ggml-large-v2.bin` model and Silero VAD model
- **ffmpeg** — for audio format conversion
- **Zoom local recordings** — stored in `~/Documents/Zoom/`

## Customization Points

- **Model**: Change the whisper model path for speed vs. accuracy trade-off
- **Zoom folder**: Change `~/Documents/Zoom/` if recordings are stored elsewhere
- **Meeting notes location**: The skill auto-detects; create the file where you want it
