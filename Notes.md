## [SPIKE] Get subtitles data

## Using third party text translator or audio to text translators

Examples of services and APIs that provide automatic speech recognition (ASR) or natural language processing (NLP) capabilities

- Google Cloud Speech-to-Text

- IBM Watson Speech to Text

- Wit.ai: A natural language processing platform that offers speech recognition as part of its capabilities. It's now owned by Facebook.

## Using netflix subtitles

Inspecting an extension code we found that the extension likely fetches subtitle data from Netflix's internal structures or APIs

### Findings

- #### Netflix tech blogs

  Netflix has a few tech blogs related to subtitles  
   [Implementing Japanese Subtitles on Netflix](https://netflixtechblog.com/implementing-japanese-subtitles-on-netflix-c165fbe61989)  
   [Introducing Netflix Timed Text Authoring Lineage](https://netflixtechblog.com/introducing-netflix-timed-text-authoring-lineage-6fb57b72ad41)

- #### Netflix AI Model to Simplify Subtitles for Translation

  [Netflix Builds Proof-of-Concept AI Model to Simplify Subtitles for Translation](https://developer.nvidia.com/blog/how-netflix-uses-ai-to-simplify-subtitles-for-translation-updated/#)

  To help localize subtitles from English to other languages, such as Russian, Spanish, or Portuguese, Netflix developed a proof-of-concept AI model that can automatically simplify and translate subtitles to multiple languages.

  The work is presented in a paper, [Simplify-then-Translate: Automatic Preprocessing for Black-Box Machine Translation](https://arxiv.org/abs/2005.11197), published this month on the preprint platform arXiv. The work is a collaboration between Netflix and Virginia Tech.

  https://arxiv.org/pdf/2005.11197.pdf

- #### Subtitle formats

  WebVTT (Web Video Text Tracks), SRT (SubRip Subtitle), and TTML (Timed Text Markup Language) are all subtitle formats commonly used in the context of web and video streaming. Each format has its own structure and syntax, but they all serve the purpose of encoding timed text information for subtitles or captions.

  WebVTT (Web Video Text Tracks):

  Format: WebVTT is a simple text-based format with a timecode associated with each subtitle cue.
  Example:

  ```bash
  00:00:00.000 --> 00:00:02.500
  This is the first subtitle cue.

  00:00:03.000 --> 00:00:05.000
  This is the second subtitle cue.
  ```

  SRT (SubRip Subtitle):

  Format: SRT is another text-based subtitle format with a timecode for each subtitle.
  Example:

  ```bash
  1
  00:00:01,000 --> 00:00:04,000
  This is the first subtitle.

  2
  00:00:05,000 --> 00:00:08,000
  This is the second subtitle.
  ```

  TTML (Timed Text Markup Language):

  Format: TTML is an XML-based format for representing timed text. It allows for more complex styling and formatting compared to plain text formats like WebVTT and SRT.
  Example:

  ```xml
  <tt xmlns="http://www.w3.org/ns/ttml">
    <body>
      <div>
        <p begin="00:00:01.000" end="00:00:04.000">This is the first subtitle.</p>
      </div>
      <div>
        <p begin="00:00:05.000" end="00:00:08.000">This is the second subtitle.</p>
      </div>
    </body>
  </tt>
  ```

- #### Manifests
  The extension seems to manage subtitle data by storing manifests (which include information about subtitles) in the browser's local storage

### Learnings form inspecting netflix site

- No files with subtitle file extensions (.sub .idx .ass .ssa .vtt) or file type matching subtitles was found
- Examine WebSocket Connections - no web socket contained any messages related to subtitles, its very unlikely subtitles are received via websockets
- Netflix uses Digital Rights Management (DRM) to protect its content. This can make reverse engineering more challenging, as some requests and scripts may be encrypted or obfuscated.
- Netflix typically uses a combination of technologies to deliver subtitles, and the actual subtitle data might **not be** directly visible in the network calls or in easily recognizable formats like JSON
- Netflix often embeds subtitles directly into the video stream. This means that the subtitle text is included as part of the video file, and it's not fetched separately. In such cases, you won't see a separate network request for subtitles. (This needs to be checked)
-

---
