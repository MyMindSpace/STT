Real-time Speech-to-Text with AssemblyAI and PyAudio
This project is a real-time speech-to-text transcription system that streams audio from your microphone to AssemblyAI’s Streaming API
 using WebSockets. The program captures audio through the microphone, streams it to AssemblyAI, receives live transcription, and saves the recorded audio to a .wav file after the session ends.

* Features
1. Real-time speech recognition using AssemblyAI Streaming API
2. Captures audio through the microphone with PyAudio
3. Streams audio in 50ms chunks over WebSocket
4. Handles live formatted and unformatted transcripts
5. Records audio locally and saves as a .wav file with timestamp
6. Clean resource management and error handling

* How This Was Built
1. Audio Capture
Used pyaudio to capture microphone input.
Configured sample rate at 16kHz, mono channel, 16-bit PCM format.

2. WebSocket Streaming
Established connection with AssemblyAI Streaming endpoint.
Sent binary audio frames in real-time to the API.

3. Transcription Handling
Processed incoming JSON responses.
Displayed interim transcripts and formatted text when available.

4. Recording and Saving Audio
Stored raw audio frames in memory while streaming.
Saved all captured audio into a .wav file when the session ended.

5. Requirements
Python 3.8 or above
A valid AssemblyAI API Key

6. Installation
Clone this repository or copy the code into a Python file (e.g., realtime_stt.py).
Install required dependencies:
  pip install pyaudio websocket-client
Replace the placeholder API key in the code:
  API_KEY = "your_api_key_here"

* Usage
Run the script in your terminal:

python realtime_stt.py

Speak into your microphone.
Live transcripts will appear in the terminal.
Audio will continue recording until you stop the program.
Stop the program with Ctrl + C.
A termination message is sent to the server.
The recorded audio will be saved locally as a .wav file with a timestamp.

* Implementation Details
1. Audio Configuration
Frames per buffer: 800 samples (~50ms at 16kHz)
Sample rate: 16000 Hz
Format: 16-bit PCM (pyaudio.paInt16)
Channels: Mono (1)

2. Concurrency
Audio streaming is handled in a dedicated thread.
The main thread listens for WebSocket events and manages graceful termination.

3. Error Handling
Robust error messages for audio device issues, WebSocket disconnects, and JSON decoding errors.
Ensures all audio streams and threads are cleaned up on exit.

* Notes
Ensure your microphone is accessible and not in use by other applications.
Network stability is important for uninterrupted streaming.
The saved .wav file is raw audio; it does not contain transcripts.
