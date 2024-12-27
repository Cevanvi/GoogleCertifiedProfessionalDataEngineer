### Question 1

How can you use Cloud ML APIs to identify and track objects in a video?

1. [ ] Split the video into a series of image files, then send them through the Cloud Vision API requesting the
   LABEL_DETECTION feature.
2. [ ] Split the video into a series of image files, then send them through the Cloud Vision API requesting the
   OBJECT_LOCALIZATION feature.
3. [ ] Manually track the movement of objects, but send a reference image of each individual object through the Cloud
   Vision API requesting the LABEL_DETECTION feature.
4. [x] Send the video through the Cloud Video Intelligence API, requesting the OBJECT_TRACKING feature.

<details>
  <summary>NOTE</summary>

```
Object tracking tracks multiple objects detected in an input video.
To make an object tracking request, call the annotate method and specify OBJECT_TRACKING in the features field.
```

</details>

### Question 2

If you make a request to the documents:analyzeEntities endpoint of the Natural Language API, what sort of information
can you expect in the response?

1. [ ] An array of Entity objects that will each contain the name of the object as a string.
2. [ ] An array of strings for each object detected in the document.
3. [ ] An array of Entity objects that will each contain metadata including link to a relevant Google Search of that
   object.
4. [x] An array of Entity objects that will each contain metadata including a Wikipedia URL and Knowledge Graph MID, if
   available.

<details>
  <summary>NOTE</summary>

```
Entity Analysis inspects the given text for known entities (proper nouns such as public figures, landmarks, etc.), and returns information about those entities.


```

</details>

### Question 3

How would you begin to design a Dialogflow agent that can answer requests for weather forecasts?

1. [ ] Create an Intent for requesting a weather forecast, let Dialogflow generate training phrases and structured
   parameters that can be used to create a response.
2. [x] Create an Intent for requesting a weather forecast, specify training phrases based on real-world speech patterns
   that would ask this question, and define the structured parameters that can be used to create a response.
3. [ ] Create an Intent for requesting a weather forecast, let Dialogflow generate training phrases, and define the
   structured parameters that can be used to create a response.
4. [ ] Create an Intent for requesting a weather forecast, specify every combination of words that could constitute the
   request, let Dialogflow infer structured parameters that can be used to create a response.

<details>
  <summary>NOTE</summary>

```
An intent categorizes an end-user's intention for one conversation turn.
Training phrases are example phrases for what end-users might say.
When building an agent, you control how data is extracted by annotating parts of your training phrases 
and configuring the associated parameters.
```

</details>

### Question 4

How do you provide GCP authentication credentials when making request to Cloud MP APIs from the command line with curl?

1. [ ] Call curl from inside a bash script with hard-coded credentials.
2. [ ] Enter your GCP username and password manually when prompted by the request.
3. [ ] Use the credentials in a service account key JSON file by encoding these in the HTTP request.
4. [x] Configure authentication with gcloud, then use 'print-access-token' to include an authorization bearer in the
   HTTP request.

<details>
  <summary>NOTE</summary>

```
The gcloud tool must be properly configured and authenticated.
It can then be used to generate access tokens which can be included in the header of the HTTP request.
```

</details>

### Question 5

What would be the most efficient way to transcribe audio from an input video while also filtering out profanity?

1. [ ] Extract the audio track from the video and use the Cloud Speech to Text API, setting profanityFilter to true in
   the RecognitionConfig.
2. [x] Use the Cloud Video Intelligence API, requesting the SPEECH_TRANSCRIPTION feature, and set filterProfanity to
   true in the speechTranscriptionConfig.
3. [ ] Extract the audio track from the video and use the Cloud Speech to Text API, but manually edit our profanity as
   this is not a feature of the API.
4. [ ] Use the Cloud Video Intelligence API, but manually edit our profanity as this is not a feature of the API.

<details>
  <summary>NOTE</summary>

```
The Video Intelligence API can transcribe speech to text from supported video files.
Use the filterProfanity option to filter out known profanities in transcriptions.
Matched words are replaced with the leading character of the word followed by asterisks.
```

</details>

### Question 6

Which features could you include in your request to the Cloud Vision API to detect text in images?

1. [ ] LETTER_DETECTION
2. [x] DOCUMENT_TEXT_DETECTION
3. [x] TEXT_DETECTION
4. [ ] LABEL_DETECTION
5. [ ] LOGO_DETECTION

<details>
  <summary>NOTE</summary>

```
TEXT_DETECTION detects and extracts text from any image.
DOCUMENT_TEXT_DETECTION also extracts text from an image, but the response is optimized for dense text and documents.
```

</details>

### Question 7

What would be the best approach to transcribing a conversation from a recorded telephone call?

1. [ ] Use synchronous speech recognition. Set enableSpeakerDiarization to true and the model to 'phone_call' in the
   RecognitionConfig.
2. [ ] Use synchronous speech recognition. Set enableSpeakerDiarization to false and the model to 'phone_call' in the
   RecognitionConfig.
3. [x] Use asynchronous speech recognition. Set enableSpeakerDiarization to true and the model to 'phone_call' in the
   RecognitionConfig.
4. [ ] Use asynchronous speech recognition. Set enableSpeakerDiarization to false and the model to 'phone_call' in the
   RecognitionConfig.

<details>
  <summary>NOTE</summary>

```
Speech-to-Text can recognize multiple speakers in the same audio clip using Speaker Diarization.
Use asynchronous speech recognition to recognize audio that is longer than a minute.
```

</details>

### Question 8

What are some of the properties that can be returned by the Cloud Vision API when requesting the FACE_DETECTION feature?

1. [ ] Bounding boxes for all faces in the image, as well as Machine-Generated Identifier (MID) matches of faces from
   Google Knowledge Graph
2. [ ] Positions of the features of the face (eg. eyes and noise), likelihood of certain emotions, estimation of age
3. [x] Positions of the features of the face (eg. eyes and noise), likelihood of certain emotions, likelihood of
   headwear
4. [ ] Bounding boxes for all faces in the image, as well as best-guess matches of faces from social media and Google
   Images

<details>
  <summary>NOTE</summary>

```
Face Detection detects multiple faces within an image along with the associated key facial 
attributes such as emotional state or wearing headwear. Specific individual Facial Recognition is not supported.
```

</details>

### Question 9

What categories are returned in the safeSearchAnnotation response from the Cloud Vision API?

1. [x] Adult, Spoof, Medical, Violence, Racy
2. [ ] Adult, Meme, Medical, Danger, Racy
3. [ ] Safe for Work, Not Safe for Work
4. [ ] General Audiences, PG-13, Mature

<details>
  <summary>NOTE</summary>

```
SafeSearch Detection detects explicit content such as adult content or violent content within an image.
This feature uses five categories (adult, spoof, medical, violence, and racy) and returns the likelihood that
each is present in a given image.
```

</details>

### Question 10

How should you interpret the documentSentiment response from the Natural Language API?

1. [ ] 'score' represents an overall emotional leaning of a test from -1.0 (negative) to 1.0 (positive), and 'magnitude'
   indicates the overall strength of emotion. 'magnitude' is normalized so the length of the text is not a factor.
2. [ ] 'magnitude' represents an overall emotional leaning of a test from -1.0 (negative) to 1.0 (positive), and 'score'
   indicates the overall strength of emotion. 'score' is normalized so the length of the text is not a factor.
3. [x] 'score' represents an overall emotional leaning of a test from -1.0 (negative) to 1.0 (positive), and 'magnitude'
   indicates the overall strength of emotion. 'magnitude' is not normalized so longer text blocks may have greater
   magnitudes.
4. [ ] 'magnitude' represents an overall emotional leaning of a test from -1.0 (negative) to 1.0 (positive), and 'score'
   indicates the overall strength of emotion. 'score' is not normalized so longer text blocks may have greater
   magnitudes.

<details>
  <summary>NOTE</summary>

```
A response value to the Gettysburg Address of 0.2 score indicates a document which is slightly positive in emotion,
while the value of 3.6 indicates a relatively emotional document, given its small size (of about a paragraph).
Note that the first sentence of the Gettysburg address contains a very high positive score of 0.8.
```

</details>
