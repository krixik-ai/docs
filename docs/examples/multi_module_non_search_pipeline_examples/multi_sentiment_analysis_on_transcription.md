## Multi-Module Pipeline: Sentiment Analysis on Transcription

This document details a modular pipeline that takes in an audio file in English, [`transcribes`](../../modules/ai_modules/transcribe_module.md) it, and then performs [`sentiment analysis`](../../modules/ai_modules/sentiment_module.md) on each sentence of the transcript.

The document is divided into the following sections:

- [Pipeline Setup](#pipeline-setup)
- [Processing an Input File](#processing-an-input-file)

### Pipeline Setup

To achieve what we've described above, let's set up a pipeline sequentially consisting of the following modules:

- A [`transcribe`](../../modules/ai_modules/transcribe_module.md) module.

- A [`json-to-txt`](../../modules/support_function_modules/json-to-txt_module.md) module.

- A [`parser`](../../modules/support_function_modules/parser_module.md) module.

- A [`sentiment`](../../modules/ai_modules/sentiment_module.md) module.

We use the [`json-to-txt`](../../modules/support_function_modules/json-to-txt_module.md) and [`parser`](../../modules/support_function_modules/parser_module.md) combination, which combines the transcribed snippets into one document and then splices it again, to make sure that any pauses in speech don't make for partial snippets that can confuse the [`sentiment`](../../modules/ai_modules/sentiment_module.md) model.

Pipeline setup is accomplished through the [`.create_pipeline`](../../system/pipeline_creation/create_pipeline.md) method, as follows:


```python
# create a pipeline as detailed above
pipeline = krixik.create_pipeline(name="multi_sentiment_analysis_on_transcription",
                                  module_chain=["transcribe",
                                                "json-to-txt",
                                                "parser",
                                                "sentiment"])
```

### Processing an Input File

Lets take a quick look at a short test file before processing.


```python
# examine contents of input file
import IPython
IPython.display.Audio("../../../data/input/Interesting Facts About Colombia.mp3")
```





<audio  controls="controls" >
    Your browser does not support the audio element.
</audio>




We will use the default models for every module in the pipeline, so the [`modules`](../../system/parameters_processing_files_through_pipelines/process_method.md#selecting-models-via-the-modules-argument) argument of the [`.process`](../../system/parameters_processing_files_through_pipelines/process_method.md) method doesn't need to be leveraged.


```python
# process the file through the pipeline, as described above
process_output = pipeline.process(local_file_path = "../../../data/input/Interesting Facts About Colombia.mp3", # the initial local filepath where the input file is stored
                                  local_save_directory="../../../data/output", # the local directory that the output file will be saved to
                                  expire_time=60*30, # process data will be deleted from the Krixik system in 30 minutes
                                  wait_for_process=True, # wait for process to complete before returning IDE control to user
                                  verbose=False) # do not display process update printouts upon running code
```

The output of this process is printed below. To learn more about each component of the output, review documentation for the [`.process`](../../system/parameters_processing_files_through_pipelines/process_method.md) method.

Because the output of this particular module-model pair is a JSON file, the process output is provided in this object as well (this is only the case for JSON outputs).  Moreover, the output file itself has been saved to the location noted in the `process_output_files` key.  The `file_id` of the processed input is used as a filename prefix for the output file.


```python
# nicely print the output of this process
print(json.dumps(process_output, indent=2))
```

    {
      "status_code": 200,
      "pipeline": "multi_sentiment_analysis_on_transcription",
      "request_id": "54a8f094-ef67-403c-8fbb-5497bd72480a",
      "file_id": "39b7b21d-d65d-474e-8ddc-14f6dff9b060",
      "message": "SUCCESS - output fetched for file_id 39b7b21d-d65d-474e-8ddc-14f6dff9b060.Output saved to location(s) listed in process_output_files.",
      "warnings": [],
      "process_output": [
        {
          "snippet": " That's episode looking at the great country of Columbia.",
          "positive": 0.992,
          "negative": 0.008,
          "neutral": 0.0
        },
        {
          "snippet": "We looked at some really basic facts.",
          "positive": 0.252,
          "negative": 0.748,
          "neutral": 0.0
        },
        {
          "snippet": "It's name, a bit of its history, the type of people that live there, land size and all that jazz.",
          "positive": 0.998,
          "negative": 0.002,
          "neutral": 0.0
        },
        {
          "snippet": "But in this video, we're gonna go into a little bit more of a detailed look.",
          "positive": 0.99,
          "negative": 0.01,
          "neutral": 0.0
        },
        {
          "snippet": "Yo, what is going on guys?",
          "positive": 0.005,
          "negative": 0.995,
          "neutral": 0.0
        },
        {
          "snippet": "Welcome back to F2D facts.",
          "positive": 0.999,
          "negative": 0.001,
          "neutral": 0.0
        },
        {
          "snippet": "The channel where I look at people cultures and places, my name is Dave Wouple.",
          "positive": 0.918,
          "negative": 0.082,
          "neutral": 0.0
        },
        {
          "snippet": "And today we are gonna be looking more at Columbia in our Columbia Part 2 video.",
          "positive": 0.015,
          "negative": 0.985,
          "neutral": 0.0
        },
        {
          "snippet": "Which just reminds me guys, this is part of our Columbia playlist.",
          "positive": 0.997,
          "negative": 0.003,
          "neutral": 0.0
        },
        {
          "snippet": "I'll put it down in the description box below and I'll talk about that more at the end of the video.",
          "positive": 0.004,
          "negative": 0.996,
          "neutral": 0.0
        },
        {
          "snippet": "But if you're new here, join me every single Monday to learn about new countries from around the world.",
          "positive": 0.999,
          "negative": 0.001,
          "neutral": 0.0
        },
        {
          "snippet": "You can do that by hitting that subscribe and that belt notification button.",
          "positive": 0.016,
          "negative": 0.984,
          "neutral": 0.0
        },
        {
          "snippet": "But that skits.",
          "positive": 0.024,
          "negative": 0.976,
          "neutral": 0.0
        }
      ],
      "process_output_files": [
        "../../../data/output/39b7b21d-d65d-474e-8ddc-14f6dff9b060.json"
      ]
    }


To confirm that everything went as it should have, let's load in the text file output from `process_output_files`:


```python
# load in process output from file
with open(process_output["process_output_files"][0]) as f:
  print(json.dumps(json.load(f), indent=2))
```

    [
      {
        "snippet": " That's episode looking at the great country of Columbia.",
        "positive": 0.992,
        "negative": 0.008,
        "neutral": 0.0
      },
      {
        "snippet": "We looked at some really basic facts.",
        "positive": 0.252,
        "negative": 0.748,
        "neutral": 0.0
      },
      {
        "snippet": "It's name, a bit of its history, the type of people that live there, land size and all that jazz.",
        "positive": 0.998,
        "negative": 0.002,
        "neutral": 0.0
      },
      {
        "snippet": "But in this video, we're gonna go into a little bit more of a detailed look.",
        "positive": 0.99,
        "negative": 0.01,
        "neutral": 0.0
      },
      {
        "snippet": "Yo, what is going on guys?",
        "positive": 0.005,
        "negative": 0.995,
        "neutral": 0.0
      },
      {
        "snippet": "Welcome back to F2D facts.",
        "positive": 0.999,
        "negative": 0.001,
        "neutral": 0.0
      },
      {
        "snippet": "The channel where I look at people cultures and places, my name is Dave Wouple.",
        "positive": 0.918,
        "negative": 0.082,
        "neutral": 0.0
      },
      {
        "snippet": "And today we are gonna be looking more at Columbia in our Columbia Part 2 video.",
        "positive": 0.015,
        "negative": 0.985,
        "neutral": 0.0
      },
      {
        "snippet": "Which just reminds me guys, this is part of our Columbia playlist.",
        "positive": 0.997,
        "negative": 0.003,
        "neutral": 0.0
      },
      {
        "snippet": "I'll put it down in the description box below and I'll talk about that more at the end of the video.",
        "positive": 0.004,
        "negative": 0.996,
        "neutral": 0.0
      },
      {
        "snippet": "But if you're new here, join me every single Monday to learn about new countries from around the world.",
        "positive": 0.999,
        "negative": 0.001,
        "neutral": 0.0
      },
      {
        "snippet": "You can do that by hitting that subscribe and that belt notification button.",
        "positive": 0.016,
        "negative": 0.984,
        "neutral": 0.0
      },
      {
        "snippet": "But that skits.",
        "positive": 0.024,
        "negative": 0.976,
        "neutral": 0.0
      }
    ]
