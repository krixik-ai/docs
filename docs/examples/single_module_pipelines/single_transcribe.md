## Single-Module Pipeline: `transcribe`

This document is a walkthrough of how to assemble and use a single-module pipeline that only includes a [`transcribe`](../../modules/ai_modules/transcribe_module.md) module. It is divided into the following sections:

- [Pipeline Setup](#pipeline-setup)
- [Required Input Format](#required-input-format)
- [Using the Default Model](#using-the-default-model)
- [Using a Non-Default Model](#using-a-non-default-model)

### Pipeline Setup

Let's first instantiate a single-module [`transcribe`](../../modules/ai_modules/transcribe_module.md)  pipeline.

We use the [`.create_pipeline`](../../system/pipeline_creation/create_pipeline.md) method for this, passing only the [`transcribe`](../../modules/ai_modules/transcribe_module.md)  module name into `module_chain`.


```python
# create a pipeline with a single transcribe module
pipeline = krixik.create_pipeline(name="single_transcribe_1",
                                  module_chain=["transcribe"])
```

### Required Input Format

The [`transcribe`](../../modules/ai_modules/transcribe_module.md)  module accepts audio inputs. Acceptable file formats are only MP3 for the time being.

Let's take a quick look at a valid input file, and then process it.


```python
# examine contents of input file
import IPython
IPython.display.Audio("../../../data/input/Interesting Facts About Colombia.mp3")
```





<audio  controls="controls" >
    Your browser does not support the audio element.
</audio>




### Using the Default Model

Let's process our test input file using the [`transcribe`](../../modules/ai_modules/transcribe_module.md)  module's [default model](../../modules/ai_modules/transcribe_module.md#available-models-in-the-transcribe-module) : [`whisper-tiny`](https://huggingface.co/openai/whisper-tiny).

Given that this is the default model, we need not specify model selection through the optional [`modules`](../../system/parameters_processing_files_through_pipelines/process_method.md#selecting-models-via-the-modules-argument) argument in the [`.process`](../../system/parameters_processing_files_through_pipelines/process_method.md) method.


```python
# process the file with the default model
process_output = pipeline.process(local_file_path="../../../data/input/Interesting Facts About Colombia.mp3", # the initial local filepath where the input file is stored
                                  local_save_directory="../../../data/output", # the local directory that the output file will be saved to
                                  expire_time=60 * 30, # process data will be deleted from the Krixik system in 30 minutes
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
      "pipeline": "single_transcribe_1",
      "request_id": "10292c9b-1ae6-40c6-a368-9305cf71d031",
      "file_id": "a04dc5d6-ac61-486e-8794-8c5ac3cf420f",
      "message": "SUCCESS - output fetched for file_id a04dc5d6-ac61-486e-8794-8c5ac3cf420f.Output saved to location(s) listed in process_output_files.",
      "warnings": [],
      "process_output": [
        {
          "transcript": " That's episode looking at the great country of Columbia. We looked at some really basic facts. It's name, a bit of its history, the type of people that live there, land size and all that jazz. But in this video, we're gonna go into a little bit more of a detailed look. Yo, what is going on guys? Welcome back to F2D facts. The channel where I look at people cultures and places, my name is Dave Wouple. And today we are gonna be looking more at Columbia in our Columbia Part 2 video. Which just reminds me guys, this is part of our Columbia playlist. I'll put it down in the description box below and I'll talk about that more at the end of the video. But if you're new here, join me every single Monday to learn about new countries from around the world. You can do that by hitting that subscribe and that belt notification button. But that skits.",
          "timestamped_transcript": [
            {
              "id": 0,
              "start": 0.0,
              "end": 2.14,
              "text": " That's episode looking at the great country of Columbia.",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.684,
              "words": [
                {
                  "text": "That's",
                  "start": 0.0,
                  "end": 0.36,
                  "confidence": 0.332
                },
                {
                  "text": "episode",
                  "start": 0.36,
                  "end": 0.5,
                  "confidence": 0.377
                },
                {
                  "text": "looking",
                  "start": 0.5,
                  "end": 0.82,
                  "confidence": 0.844
                },
                {
                  "text": "at",
                  "start": 0.82,
                  "end": 1.02,
                  "confidence": 0.996
                },
                {
                  "text": "the",
                  "start": 1.02,
                  "end": 1.12,
                  "confidence": 0.986
                },
                {
                  "text": "great",
                  "start": 1.12,
                  "end": 1.32,
                  "confidence": 0.97
                },
                {
                  "text": "country",
                  "start": 1.32,
                  "end": 1.68,
                  "confidence": 0.986
                },
                {
                  "text": "of",
                  "start": 1.68,
                  "end": 1.8,
                  "confidence": 0.98
                },
                {
                  "text": "Columbia.",
                  "start": 1.8,
                  "end": 2.14,
                  "confidence": 0.692
                }
              ]
            },
            {
              "id": 1,
              "start": 2.2,
              "end": 4.26,
              "text": " We looked at some really basic facts.",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.905,
              "words": [
                {
                  "text": "We",
                  "start": 2.2,
                  "end": 2.36,
                  "confidence": 0.995
                },
                {
                  "text": "looked",
                  "start": 2.36,
                  "end": 2.62,
                  "confidence": 0.989
                },
                {
                  "text": "at",
                  "start": 2.62,
                  "end": 2.74,
                  "confidence": 0.999
                },
                {
                  "text": "some",
                  "start": 2.74,
                  "end": 3.0,
                  "confidence": 0.998
                },
                {
                  "text": "really",
                  "start": 3.0,
                  "end": 3.3,
                  "confidence": 0.988
                },
                {
                  "text": "basic",
                  "start": 3.3,
                  "end": 3.88,
                  "confidence": 0.515
                },
                {
                  "text": "facts.",
                  "start": 3.88,
                  "end": 4.26,
                  "confidence": 0.994
                }
              ]
            },
            {
              "id": 2,
              "start": 4.26,
              "end": 5.9,
              "text": " It's name, a bit of its history,",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.961,
              "words": [
                {
                  "text": "It's",
                  "start": 4.26,
                  "end": 4.58,
                  "confidence": 0.943
                },
                {
                  "text": "name,",
                  "start": 4.58,
                  "end": 4.94,
                  "confidence": 0.937
                },
                {
                  "text": "a",
                  "start": 4.98,
                  "end": 5.1,
                  "confidence": 0.984
                },
                {
                  "text": "bit",
                  "start": 5.1,
                  "end": 5.2,
                  "confidence": 0.995
                },
                {
                  "text": "of",
                  "start": 5.2,
                  "end": 5.32,
                  "confidence": 0.995
                },
                {
                  "text": "its",
                  "start": 5.32,
                  "end": 5.54,
                  "confidence": 0.897
                },
                {
                  "text": "history,",
                  "start": 5.54,
                  "end": 5.9,
                  "confidence": 0.999
                }
              ]
            },
            {
              "id": 3,
              "start": 6.28,
              "end": 7.46,
              "text": " the type of people that live there,",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.894,
              "words": [
                {
                  "text": "the",
                  "start": 6.28,
                  "end": 6.4,
                  "confidence": 0.921
                },
                {
                  "text": "type",
                  "start": 6.4,
                  "end": 6.52,
                  "confidence": 0.981
                },
                {
                  "text": "of",
                  "start": 6.52,
                  "end": 6.64,
                  "confidence": 0.997
                },
                {
                  "text": "people",
                  "start": 6.64,
                  "end": 6.82,
                  "confidence": 0.999
                },
                {
                  "text": "that",
                  "start": 6.82,
                  "end": 6.96,
                  "confidence": 0.994
                },
                {
                  "text": "live",
                  "start": 6.96,
                  "end": 7.22,
                  "confidence": 0.53
                },
                {
                  "text": "there,",
                  "start": 7.22,
                  "end": 7.46,
                  "confidence": 0.96
                }
              ]
            },
            {
              "id": 4,
              "start": 7.46,
              "end": 9.24,
              "text": " land size and all that jazz.",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.788,
              "words": [
                {
                  "text": "land",
                  "start": 7.46,
                  "end": 7.86,
                  "confidence": 0.653
                },
                {
                  "text": "size",
                  "start": 7.86,
                  "end": 8.28,
                  "confidence": 0.748
                },
                {
                  "text": "and",
                  "start": 8.28,
                  "end": 8.48,
                  "confidence": 0.504
                },
                {
                  "text": "all",
                  "start": 8.48,
                  "end": 8.68,
                  "confidence": 0.998
                },
                {
                  "text": "that",
                  "start": 8.68,
                  "end": 8.94,
                  "confidence": 0.981
                },
                {
                  "text": "jazz.",
                  "start": 8.94,
                  "end": 9.24,
                  "confidence": 0.993
                }
              ]
            },
            {
              "id": 5,
              "start": 9.52,
              "end": 10.68,
              "text": " But in this video, we're gonna go into",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.909,
              "words": [
                {
                  "text": "But",
                  "start": 9.52,
                  "end": 9.64,
                  "confidence": 0.997
                },
                {
                  "text": "in",
                  "start": 9.64,
                  "end": 9.72,
                  "confidence": 0.993
                },
                {
                  "text": "this",
                  "start": 9.72,
                  "end": 9.86,
                  "confidence": 0.999
                },
                {
                  "text": "video,",
                  "start": 9.86,
                  "end": 10.1,
                  "confidence": 0.999
                },
                {
                  "text": "we're",
                  "start": 10.14,
                  "end": 10.26,
                  "confidence": 0.924
                },
                {
                  "text": "gonna",
                  "start": 10.26,
                  "end": 10.36,
                  "confidence": 0.537
                },
                {
                  "text": "go",
                  "start": 10.36,
                  "end": 10.5,
                  "confidence": 0.984
                },
                {
                  "text": "into",
                  "start": 10.5,
                  "end": 10.68,
                  "confidence": 0.946
                }
              ]
            },
            {
              "id": 6,
              "start": 10.68,
              "end": 12.56,
              "text": " a little bit more of a detailed look.",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.996,
              "words": [
                {
                  "text": "a",
                  "start": 10.68,
                  "end": 10.94,
                  "confidence": 1.0
                },
                {
                  "text": "little",
                  "start": 10.94,
                  "end": 11.14,
                  "confidence": 0.996
                },
                {
                  "text": "bit",
                  "start": 11.14,
                  "end": 11.26,
                  "confidence": 0.991
                },
                {
                  "text": "more",
                  "start": 11.26,
                  "end": 11.6,
                  "confidence": 0.999
                },
                {
                  "text": "of",
                  "start": 11.6,
                  "end": 11.74,
                  "confidence": 0.995
                },
                {
                  "text": "a",
                  "start": 11.74,
                  "end": 11.9,
                  "confidence": 0.997
                },
                {
                  "text": "detailed",
                  "start": 11.9,
                  "end": 12.22,
                  "confidence": 0.996
                },
                {
                  "text": "look.",
                  "start": 12.22,
                  "end": 12.56,
                  "confidence": 0.998
                }
              ]
            },
            {
              "id": 7,
              "start": 12.84,
              "end": 14.28,
              "text": " Yo, what is going on guys?",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.909,
              "words": [
                {
                  "text": "Yo,",
                  "start": 12.84,
                  "end": 13.02,
                  "confidence": 0.832
                },
                {
                  "text": "what",
                  "start": 13.26,
                  "end": 13.36,
                  "confidence": 0.995
                },
                {
                  "text": "is",
                  "start": 13.36,
                  "end": 13.48,
                  "confidence": 0.986
                },
                {
                  "text": "going",
                  "start": 13.48,
                  "end": 13.7,
                  "confidence": 0.96
                },
                {
                  "text": "on",
                  "start": 13.7,
                  "end": 13.92,
                  "confidence": 1.0
                },
                {
                  "text": "guys?",
                  "start": 13.92,
                  "end": 14.28,
                  "confidence": 0.719
                }
              ]
            },
            {
              "id": 8,
              "start": 14.36,
              "end": 15.72,
              "text": " Welcome back to F2D facts.",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.701,
              "words": [
                {
                  "text": "Welcome",
                  "start": 14.36,
                  "end": 14.6,
                  "confidence": 0.99
                },
                {
                  "text": "back",
                  "start": 14.6,
                  "end": 14.82,
                  "confidence": 0.999
                },
                {
                  "text": "to",
                  "start": 14.82,
                  "end": 15.02,
                  "confidence": 0.991
                },
                {
                  "text": "F2D",
                  "start": 15.02,
                  "end": 15.4,
                  "confidence": 0.601
                },
                {
                  "text": "facts.",
                  "start": 15.4,
                  "end": 15.72,
                  "confidence": 0.391
                }
              ]
            },
            {
              "id": 9,
              "start": 15.72,
              "end": 16.96,
              "text": " The channel where I look at people cultures",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.833,
              "words": [
                {
                  "text": "The",
                  "start": 15.72,
                  "end": 15.86,
                  "confidence": 0.504
                },
                {
                  "text": "channel",
                  "start": 15.86,
                  "end": 16.02,
                  "confidence": 0.894
                },
                {
                  "text": "where",
                  "start": 16.02,
                  "end": 16.16,
                  "confidence": 0.994
                },
                {
                  "text": "I",
                  "start": 16.16,
                  "end": 16.24,
                  "confidence": 0.99
                },
                {
                  "text": "look",
                  "start": 16.24,
                  "end": 16.38,
                  "confidence": 0.997
                },
                {
                  "text": "at",
                  "start": 16.38,
                  "end": 16.48,
                  "confidence": 0.991
                },
                {
                  "text": "people",
                  "start": 16.48,
                  "end": 16.66,
                  "confidence": 0.919
                },
                {
                  "text": "cultures",
                  "start": 16.66,
                  "end": 16.96,
                  "confidence": 0.574
                }
              ]
            },
            {
              "id": 10,
              "start": 16.96,
              "end": 19.78,
              "text": " and places, my name is Dave Wouple.",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.689,
              "words": [
                {
                  "text": "and",
                  "start": 16.96,
                  "end": 17.14,
                  "confidence": 0.891
                },
                {
                  "text": "places,",
                  "start": 17.14,
                  "end": 17.5,
                  "confidence": 0.997
                },
                {
                  "text": "my",
                  "start": 17.86,
                  "end": 17.88,
                  "confidence": 0.935
                },
                {
                  "text": "name",
                  "start": 17.88,
                  "end": 18.42,
                  "confidence": 1.0
                },
                {
                  "text": "is",
                  "start": 18.42,
                  "end": 19.0,
                  "confidence": 0.919
                },
                {
                  "text": "Dave",
                  "start": 19.0,
                  "end": 19.4,
                  "confidence": 0.982
                },
                {
                  "text": "Wouple.",
                  "start": 19.4,
                  "end": 19.78,
                  "confidence": 0.36
                }
              ]
            },
            {
              "id": 11,
              "start": 19.78,
              "end": 23.66,
              "text": " And today we are gonna be looking more at Columbia",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.922,
              "words": [
                {
                  "text": "And",
                  "start": 19.78,
                  "end": 20.42,
                  "confidence": 0.989
                },
                {
                  "text": "today",
                  "start": 20.42,
                  "end": 21.1,
                  "confidence": 0.992
                },
                {
                  "text": "we",
                  "start": 21.1,
                  "end": 21.66,
                  "confidence": 0.698
                },
                {
                  "text": "are",
                  "start": 21.66,
                  "end": 22.04,
                  "confidence": 0.996
                },
                {
                  "text": "gonna",
                  "start": 22.04,
                  "end": 22.22,
                  "confidence": 0.885
                },
                {
                  "text": "be",
                  "start": 22.22,
                  "end": 22.34,
                  "confidence": 0.998
                },
                {
                  "text": "looking",
                  "start": 22.34,
                  "end": 22.62,
                  "confidence": 0.949
                },
                {
                  "text": "more",
                  "start": 22.62,
                  "end": 23.08,
                  "confidence": 0.844
                },
                {
                  "text": "at",
                  "start": 23.08,
                  "end": 23.24,
                  "confidence": 0.956
                },
                {
                  "text": "Columbia",
                  "start": 23.24,
                  "end": 23.66,
                  "confidence": 0.968
                }
              ]
            },
            {
              "id": 12,
              "start": 23.66,
              "end": 25.24,
              "text": " in our Columbia Part 2 video.",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.742,
              "words": [
                {
                  "text": "in",
                  "start": 23.66,
                  "end": 23.88,
                  "confidence": 0.655
                },
                {
                  "text": "our",
                  "start": 23.88,
                  "end": 24.02,
                  "confidence": 0.987
                },
                {
                  "text": "Columbia",
                  "start": 24.02,
                  "end": 24.28,
                  "confidence": 0.992
                },
                {
                  "text": "Part",
                  "start": 24.28,
                  "end": 24.54,
                  "confidence": 0.619
                },
                {
                  "text": "2",
                  "start": 24.54,
                  "end": 24.8,
                  "confidence": 0.434
                },
                {
                  "text": "video.",
                  "start": 24.8,
                  "end": 25.24,
                  "confidence": 0.97
                }
              ]
            },
            {
              "id": 13,
              "start": 25.72,
              "end": 27.04,
              "text": " Which just reminds me guys,",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.956,
              "words": [
                {
                  "text": "Which",
                  "start": 25.72,
                  "end": 26.0,
                  "confidence": 0.983
                },
                {
                  "text": "just",
                  "start": 26.0,
                  "end": 26.26,
                  "confidence": 0.988
                },
                {
                  "text": "reminds",
                  "start": 26.26,
                  "end": 26.7,
                  "confidence": 0.996
                },
                {
                  "text": "me",
                  "start": 26.7,
                  "end": 26.86,
                  "confidence": 0.926
                },
                {
                  "text": "guys,",
                  "start": 26.86,
                  "end": 27.04,
                  "confidence": 0.892
                }
              ]
            },
            {
              "id": 14,
              "start": 27.06,
              "end": 28.82,
              "text": " this is part of our Columbia playlist.",
              "no_speech_prob": 0.3379374146461487,
              "confidence": 0.915,
              "words": [
                {
                  "text": "this",
                  "start": 27.06,
                  "end": 27.26,
                  "confidence": 0.982
                },
                {
                  "text": "is",
                  "start": 27.26,
                  "end": 27.34,
                  "confidence": 0.982
                },
                {
                  "text": "part",
                  "start": 27.34,
                  "end": 27.54,
                  "confidence": 0.973
                },
                {
                  "text": "of",
                  "start": 27.54,
                  "end": 27.68,
                  "confidence": 0.999
                },
                {
                  "text": "our",
                  "start": 27.68,
                  "end": 27.82,
                  "confidence": 0.991
                },
                {
                  "text": "Columbia",
                  "start": 27.82,
                  "end": 28.24,
                  "confidence": 0.997
                },
                {
                  "text": "playlist.",
                  "start": 28.24,
                  "end": 28.82,
                  "confidence": 0.58
                }
              ]
            },
            {
              "id": 15,
              "start": 28.96,
              "end": 30.36,
              "text": " I'll put it down in the description box below",
              "no_speech_prob": 0.13719242811203003,
              "confidence": 0.856,
              "words": [
                {
                  "text": "I'll",
                  "start": 28.96,
                  "end": 29.06,
                  "confidence": 0.613
                },
                {
                  "text": "put",
                  "start": 29.06,
                  "end": 29.08,
                  "confidence": 0.964
                },
                {
                  "text": "it",
                  "start": 29.08,
                  "end": 29.2,
                  "confidence": 0.993
                },
                {
                  "text": "down",
                  "start": 29.2,
                  "end": 29.38,
                  "confidence": 0.998
                },
                {
                  "text": "in",
                  "start": 29.38,
                  "end": 29.54,
                  "confidence": 0.702
                },
                {
                  "text": "the",
                  "start": 29.54,
                  "end": 29.6,
                  "confidence": 0.871
                },
                {
                  "text": "description",
                  "start": 29.6,
                  "end": 29.86,
                  "confidence": 0.999
                },
                {
                  "text": "box",
                  "start": 29.86,
                  "end": 30.12,
                  "confidence": 0.984
                },
                {
                  "text": "below",
                  "start": 30.12,
                  "end": 30.36,
                  "confidence": 0.979
                }
              ]
            },
            {
              "id": 16,
              "start": 30.44,
              "end": 32.42,
              "text": " and I'll talk about that more at the end of the video.",
              "no_speech_prob": 0.13719242811203003,
              "confidence": 0.942,
              "words": [
                {
                  "text": "and",
                  "start": 30.44,
                  "end": 30.54,
                  "confidence": 0.994
                },
                {
                  "text": "I'll",
                  "start": 30.54,
                  "end": 30.68,
                  "confidence": 0.972
                },
                {
                  "text": "talk",
                  "start": 30.68,
                  "end": 30.82,
                  "confidence": 0.994
                },
                {
                  "text": "about",
                  "start": 30.82,
                  "end": 30.94,
                  "confidence": 0.983
                },
                {
                  "text": "that",
                  "start": 30.94,
                  "end": 31.1,
                  "confidence": 0.92
                },
                {
                  "text": "more",
                  "start": 31.1,
                  "end": 31.3,
                  "confidence": 0.975
                },
                {
                  "text": "at",
                  "start": 31.3,
                  "end": 31.52,
                  "confidence": 0.589
                },
                {
                  "text": "the",
                  "start": 31.52,
                  "end": 31.54,
                  "confidence": 0.984
                },
                {
                  "text": "end",
                  "start": 31.54,
                  "end": 31.7,
                  "confidence": 0.996
                },
                {
                  "text": "of",
                  "start": 31.7,
                  "end": 31.84,
                  "confidence": 0.976
                },
                {
                  "text": "the",
                  "start": 31.84,
                  "end": 31.94,
                  "confidence": 0.991
                },
                {
                  "text": "video.",
                  "start": 31.94,
                  "end": 32.42,
                  "confidence": 0.999
                }
              ]
            },
            {
              "id": 17,
              "start": 32.72,
              "end": 33.51,
              "text": " But if you're new here,",
              "no_speech_prob": 0.13719242811203003,
              "confidence": 0.99,
              "words": [
                {
                  "text": "But",
                  "start": 32.72,
                  "end": 32.84,
                  "confidence": 0.992
                },
                {
                  "text": "if",
                  "start": 32.84,
                  "end": 32.96,
                  "confidence": 0.988
                },
                {
                  "text": "you're",
                  "start": 32.96,
                  "end": 33.12,
                  "confidence": 0.983
                },
                {
                  "text": "new",
                  "start": 33.12,
                  "end": 33.24,
                  "confidence": 0.998
                },
                {
                  "text": "here,",
                  "start": 33.24,
                  "end": 33.51,
                  "confidence": 0.994
                }
              ]
            },
            {
              "id": 18,
              "start": 33.51,
              "end": 35.78,
              "text": " join me every single Monday to learn about new countries",
              "no_speech_prob": 0.13719242811203003,
              "confidence": 0.887,
              "words": [
                {
                  "text": "join",
                  "start": 33.51,
                  "end": 33.94,
                  "confidence": 0.961
                },
                {
                  "text": "me",
                  "start": 33.94,
                  "end": 34.08,
                  "confidence": 1.0
                },
                {
                  "text": "every",
                  "start": 34.08,
                  "end": 34.24,
                  "confidence": 0.912
                },
                {
                  "text": "single",
                  "start": 34.24,
                  "end": 34.46,
                  "confidence": 0.999
                },
                {
                  "text": "Monday",
                  "start": 34.46,
                  "end": 34.72,
                  "confidence": 0.967
                },
                {
                  "text": "to",
                  "start": 34.72,
                  "end": 34.82,
                  "confidence": 0.809
                },
                {
                  "text": "learn",
                  "start": 34.82,
                  "end": 35.02,
                  "confidence": 0.99
                },
                {
                  "text": "about",
                  "start": 35.02,
                  "end": 35.18,
                  "confidence": 0.671
                },
                {
                  "text": "new",
                  "start": 35.18,
                  "end": 35.38,
                  "confidence": 0.694
                },
                {
                  "text": "countries",
                  "start": 35.38,
                  "end": 35.78,
                  "confidence": 0.949
                }
              ]
            },
            {
              "id": 19,
              "start": 35.86,
              "end": 36.38,
              "text": " from around the world.",
              "no_speech_prob": 0.13719242811203003,
              "confidence": 0.992,
              "words": [
                {
                  "text": "from",
                  "start": 35.86,
                  "end": 35.98,
                  "confidence": 0.98
                },
                {
                  "text": "around",
                  "start": 35.98,
                  "end": 36.22,
                  "confidence": 0.995
                },
                {
                  "text": "the",
                  "start": 36.22,
                  "end": 36.36,
                  "confidence": 0.994
                },
                {
                  "text": "world.",
                  "start": 36.36,
                  "end": 36.38,
                  "confidence": 0.997
                }
              ]
            },
            {
              "id": 20,
              "start": 36.38,
              "end": 37.93,
              "text": " You can do that by hitting that subscribe",
              "no_speech_prob": 0.13719242811203003,
              "confidence": 0.977,
              "words": [
                {
                  "text": "You",
                  "start": 36.38,
                  "end": 36.6,
                  "confidence": 0.982
                },
                {
                  "text": "can",
                  "start": 36.6,
                  "end": 36.74,
                  "confidence": 0.998
                },
                {
                  "text": "do",
                  "start": 36.74,
                  "end": 36.84,
                  "confidence": 0.999
                },
                {
                  "text": "that",
                  "start": 36.84,
                  "end": 37.0,
                  "confidence": 0.999
                },
                {
                  "text": "by",
                  "start": 37.0,
                  "end": 37.16,
                  "confidence": 0.96
                },
                {
                  "text": "hitting",
                  "start": 37.16,
                  "end": 37.36,
                  "confidence": 0.925
                },
                {
                  "text": "that",
                  "start": 37.36,
                  "end": 37.5,
                  "confidence": 0.994
                },
                {
                  "text": "subscribe",
                  "start": 37.5,
                  "end": 37.93,
                  "confidence": 0.962
                }
              ]
            },
            {
              "id": 21,
              "start": 37.93,
              "end": 39.32,
              "text": " and that belt notification button.",
              "no_speech_prob": 0.13719242811203003,
              "confidence": 0.909,
              "words": [
                {
                  "text": "and",
                  "start": 37.93,
                  "end": 38.14,
                  "confidence": 0.938
                },
                {
                  "text": "that",
                  "start": 38.14,
                  "end": 38.32,
                  "confidence": 0.985
                },
                {
                  "text": "belt",
                  "start": 38.32,
                  "end": 38.48,
                  "confidence": 0.706
                },
                {
                  "text": "notification",
                  "start": 38.48,
                  "end": 39.04,
                  "confidence": 0.951
                },
                {
                  "text": "button.",
                  "start": 39.04,
                  "end": 39.32,
                  "confidence": 0.999
                }
              ]
            },
            {
              "id": 22,
              "start": 39.32,
              "end": 41.24,
              "text": " But that skits.",
              "no_speech_prob": 0.13719242811203003,
              "confidence": 0.759,
              "words": [
                {
                  "text": "But",
                  "start": 39.32,
                  "end": 40.36,
                  "confidence": 0.993
                },
                {
                  "text": "that",
                  "start": 40.36,
                  "end": 40.6,
                  "confidence": 0.645
                },
                {
                  "text": "skits.",
                  "start": 40.6,
                  "end": 41.24,
                  "confidence": 0.719
                }
              ]
            }
          ]
        }
      ],
      "process_output_files": [
        "../../../data/output/a04dc5d6-ac61-486e-8794-8c5ac3cf420f.json"
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
        "transcript": " That's episode looking at the great country of Columbia. We looked at some really basic facts. It's name, a bit of its history, the type of people that live there, land size and all that jazz. But in this video, we're gonna go into a little bit more of a detailed look. Yo, what is going on guys? Welcome back to F2D facts. The channel where I look at people cultures and places, my name is Dave Wouple. And today we are gonna be looking more at Columbia in our Columbia Part 2 video. Which just reminds me guys, this is part of our Columbia playlist. I'll put it down in the description box below and I'll talk about that more at the end of the video. But if you're new here, join me every single Monday to learn about new countries from around the world. You can do that by hitting that subscribe and that belt notification button. But that skits.",
        "timestamped_transcript": [
          {
            "id": 0,
            "start": 0.0,
            "end": 2.14,
            "text": " That's episode looking at the great country of Columbia.",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.684,
            "words": [
              {
                "text": "That's",
                "start": 0.0,
                "end": 0.36,
                "confidence": 0.332
              },
              {
                "text": "episode",
                "start": 0.36,
                "end": 0.5,
                "confidence": 0.377
              },
              {
                "text": "looking",
                "start": 0.5,
                "end": 0.82,
                "confidence": 0.844
              },
              {
                "text": "at",
                "start": 0.82,
                "end": 1.02,
                "confidence": 0.996
              },
              {
                "text": "the",
                "start": 1.02,
                "end": 1.12,
                "confidence": 0.986
              },
              {
                "text": "great",
                "start": 1.12,
                "end": 1.32,
                "confidence": 0.97
              },
              {
                "text": "country",
                "start": 1.32,
                "end": 1.68,
                "confidence": 0.986
              },
              {
                "text": "of",
                "start": 1.68,
                "end": 1.8,
                "confidence": 0.98
              },
              {
                "text": "Columbia.",
                "start": 1.8,
                "end": 2.14,
                "confidence": 0.692
              }
            ]
          },
          {
            "id": 1,
            "start": 2.2,
            "end": 4.26,
            "text": " We looked at some really basic facts.",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.905,
            "words": [
              {
                "text": "We",
                "start": 2.2,
                "end": 2.36,
                "confidence": 0.995
              },
              {
                "text": "looked",
                "start": 2.36,
                "end": 2.62,
                "confidence": 0.989
              },
              {
                "text": "at",
                "start": 2.62,
                "end": 2.74,
                "confidence": 0.999
              },
              {
                "text": "some",
                "start": 2.74,
                "end": 3.0,
                "confidence": 0.998
              },
              {
                "text": "really",
                "start": 3.0,
                "end": 3.3,
                "confidence": 0.988
              },
              {
                "text": "basic",
                "start": 3.3,
                "end": 3.88,
                "confidence": 0.515
              },
              {
                "text": "facts.",
                "start": 3.88,
                "end": 4.26,
                "confidence": 0.994
              }
            ]
          },
          {
            "id": 2,
            "start": 4.26,
            "end": 5.9,
            "text": " It's name, a bit of its history,",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.961,
            "words": [
              {
                "text": "It's",
                "start": 4.26,
                "end": 4.58,
                "confidence": 0.943
              },
              {
                "text": "name,",
                "start": 4.58,
                "end": 4.94,
                "confidence": 0.937
              },
              {
                "text": "a",
                "start": 4.98,
                "end": 5.1,
                "confidence": 0.984
              },
              {
                "text": "bit",
                "start": 5.1,
                "end": 5.2,
                "confidence": 0.995
              },
              {
                "text": "of",
                "start": 5.2,
                "end": 5.32,
                "confidence": 0.995
              },
              {
                "text": "its",
                "start": 5.32,
                "end": 5.54,
                "confidence": 0.897
              },
              {
                "text": "history,",
                "start": 5.54,
                "end": 5.9,
                "confidence": 0.999
              }
            ]
          },
          {
            "id": 3,
            "start": 6.28,
            "end": 7.46,
            "text": " the type of people that live there,",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.894,
            "words": [
              {
                "text": "the",
                "start": 6.28,
                "end": 6.4,
                "confidence": 0.921
              },
              {
                "text": "type",
                "start": 6.4,
                "end": 6.52,
                "confidence": 0.981
              },
              {
                "text": "of",
                "start": 6.52,
                "end": 6.64,
                "confidence": 0.997
              },
              {
                "text": "people",
                "start": 6.64,
                "end": 6.82,
                "confidence": 0.999
              },
              {
                "text": "that",
                "start": 6.82,
                "end": 6.96,
                "confidence": 0.994
              },
              {
                "text": "live",
                "start": 6.96,
                "end": 7.22,
                "confidence": 0.53
              },
              {
                "text": "there,",
                "start": 7.22,
                "end": 7.46,
                "confidence": 0.96
              }
            ]
          },
          {
            "id": 4,
            "start": 7.46,
            "end": 9.24,
            "text": " land size and all that jazz.",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.788,
            "words": [
              {
                "text": "land",
                "start": 7.46,
                "end": 7.86,
                "confidence": 0.653
              },
              {
                "text": "size",
                "start": 7.86,
                "end": 8.28,
                "confidence": 0.748
              },
              {
                "text": "and",
                "start": 8.28,
                "end": 8.48,
                "confidence": 0.504
              },
              {
                "text": "all",
                "start": 8.48,
                "end": 8.68,
                "confidence": 0.998
              },
              {
                "text": "that",
                "start": 8.68,
                "end": 8.94,
                "confidence": 0.981
              },
              {
                "text": "jazz.",
                "start": 8.94,
                "end": 9.24,
                "confidence": 0.993
              }
            ]
          },
          {
            "id": 5,
            "start": 9.52,
            "end": 10.68,
            "text": " But in this video, we're gonna go into",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.909,
            "words": [
              {
                "text": "But",
                "start": 9.52,
                "end": 9.64,
                "confidence": 0.997
              },
              {
                "text": "in",
                "start": 9.64,
                "end": 9.72,
                "confidence": 0.993
              },
              {
                "text": "this",
                "start": 9.72,
                "end": 9.86,
                "confidence": 0.999
              },
              {
                "text": "video,",
                "start": 9.86,
                "end": 10.1,
                "confidence": 0.999
              },
              {
                "text": "we're",
                "start": 10.14,
                "end": 10.26,
                "confidence": 0.924
              },
              {
                "text": "gonna",
                "start": 10.26,
                "end": 10.36,
                "confidence": 0.537
              },
              {
                "text": "go",
                "start": 10.36,
                "end": 10.5,
                "confidence": 0.984
              },
              {
                "text": "into",
                "start": 10.5,
                "end": 10.68,
                "confidence": 0.946
              }
            ]
          },
          {
            "id": 6,
            "start": 10.68,
            "end": 12.56,
            "text": " a little bit more of a detailed look.",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.996,
            "words": [
              {
                "text": "a",
                "start": 10.68,
                "end": 10.94,
                "confidence": 1.0
              },
              {
                "text": "little",
                "start": 10.94,
                "end": 11.14,
                "confidence": 0.996
              },
              {
                "text": "bit",
                "start": 11.14,
                "end": 11.26,
                "confidence": 0.991
              },
              {
                "text": "more",
                "start": 11.26,
                "end": 11.6,
                "confidence": 0.999
              },
              {
                "text": "of",
                "start": 11.6,
                "end": 11.74,
                "confidence": 0.995
              },
              {
                "text": "a",
                "start": 11.74,
                "end": 11.9,
                "confidence": 0.997
              },
              {
                "text": "detailed",
                "start": 11.9,
                "end": 12.22,
                "confidence": 0.996
              },
              {
                "text": "look.",
                "start": 12.22,
                "end": 12.56,
                "confidence": 0.998
              }
            ]
          },
          {
            "id": 7,
            "start": 12.84,
            "end": 14.28,
            "text": " Yo, what is going on guys?",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.909,
            "words": [
              {
                "text": "Yo,",
                "start": 12.84,
                "end": 13.02,
                "confidence": 0.832
              },
              {
                "text": "what",
                "start": 13.26,
                "end": 13.36,
                "confidence": 0.995
              },
              {
                "text": "is",
                "start": 13.36,
                "end": 13.48,
                "confidence": 0.986
              },
              {
                "text": "going",
                "start": 13.48,
                "end": 13.7,
                "confidence": 0.96
              },
              {
                "text": "on",
                "start": 13.7,
                "end": 13.92,
                "confidence": 1.0
              },
              {
                "text": "guys?",
                "start": 13.92,
                "end": 14.28,
                "confidence": 0.719
              }
            ]
          },
          {
            "id": 8,
            "start": 14.36,
            "end": 15.72,
            "text": " Welcome back to F2D facts.",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.701,
            "words": [
              {
                "text": "Welcome",
                "start": 14.36,
                "end": 14.6,
                "confidence": 0.99
              },
              {
                "text": "back",
                "start": 14.6,
                "end": 14.82,
                "confidence": 0.999
              },
              {
                "text": "to",
                "start": 14.82,
                "end": 15.02,
                "confidence": 0.991
              },
              {
                "text": "F2D",
                "start": 15.02,
                "end": 15.4,
                "confidence": 0.601
              },
              {
                "text": "facts.",
                "start": 15.4,
                "end": 15.72,
                "confidence": 0.391
              }
            ]
          },
          {
            "id": 9,
            "start": 15.72,
            "end": 16.96,
            "text": " The channel where I look at people cultures",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.833,
            "words": [
              {
                "text": "The",
                "start": 15.72,
                "end": 15.86,
                "confidence": 0.504
              },
              {
                "text": "channel",
                "start": 15.86,
                "end": 16.02,
                "confidence": 0.894
              },
              {
                "text": "where",
                "start": 16.02,
                "end": 16.16,
                "confidence": 0.994
              },
              {
                "text": "I",
                "start": 16.16,
                "end": 16.24,
                "confidence": 0.99
              },
              {
                "text": "look",
                "start": 16.24,
                "end": 16.38,
                "confidence": 0.997
              },
              {
                "text": "at",
                "start": 16.38,
                "end": 16.48,
                "confidence": 0.991
              },
              {
                "text": "people",
                "start": 16.48,
                "end": 16.66,
                "confidence": 0.919
              },
              {
                "text": "cultures",
                "start": 16.66,
                "end": 16.96,
                "confidence": 0.574
              }
            ]
          },
          {
            "id": 10,
            "start": 16.96,
            "end": 19.78,
            "text": " and places, my name is Dave Wouple.",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.689,
            "words": [
              {
                "text": "and",
                "start": 16.96,
                "end": 17.14,
                "confidence": 0.891
              },
              {
                "text": "places,",
                "start": 17.14,
                "end": 17.5,
                "confidence": 0.997
              },
              {
                "text": "my",
                "start": 17.86,
                "end": 17.88,
                "confidence": 0.935
              },
              {
                "text": "name",
                "start": 17.88,
                "end": 18.42,
                "confidence": 1.0
              },
              {
                "text": "is",
                "start": 18.42,
                "end": 19.0,
                "confidence": 0.919
              },
              {
                "text": "Dave",
                "start": 19.0,
                "end": 19.4,
                "confidence": 0.982
              },
              {
                "text": "Wouple.",
                "start": 19.4,
                "end": 19.78,
                "confidence": 0.36
              }
            ]
          },
          {
            "id": 11,
            "start": 19.78,
            "end": 23.66,
            "text": " And today we are gonna be looking more at Columbia",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.922,
            "words": [
              {
                "text": "And",
                "start": 19.78,
                "end": 20.42,
                "confidence": 0.989
              },
              {
                "text": "today",
                "start": 20.42,
                "end": 21.1,
                "confidence": 0.992
              },
              {
                "text": "we",
                "start": 21.1,
                "end": 21.66,
                "confidence": 0.698
              },
              {
                "text": "are",
                "start": 21.66,
                "end": 22.04,
                "confidence": 0.996
              },
              {
                "text": "gonna",
                "start": 22.04,
                "end": 22.22,
                "confidence": 0.885
              },
              {
                "text": "be",
                "start": 22.22,
                "end": 22.34,
                "confidence": 0.998
              },
              {
                "text": "looking",
                "start": 22.34,
                "end": 22.62,
                "confidence": 0.949
              },
              {
                "text": "more",
                "start": 22.62,
                "end": 23.08,
                "confidence": 0.844
              },
              {
                "text": "at",
                "start": 23.08,
                "end": 23.24,
                "confidence": 0.956
              },
              {
                "text": "Columbia",
                "start": 23.24,
                "end": 23.66,
                "confidence": 0.968
              }
            ]
          },
          {
            "id": 12,
            "start": 23.66,
            "end": 25.24,
            "text": " in our Columbia Part 2 video.",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.742,
            "words": [
              {
                "text": "in",
                "start": 23.66,
                "end": 23.88,
                "confidence": 0.655
              },
              {
                "text": "our",
                "start": 23.88,
                "end": 24.02,
                "confidence": 0.987
              },
              {
                "text": "Columbia",
                "start": 24.02,
                "end": 24.28,
                "confidence": 0.992
              },
              {
                "text": "Part",
                "start": 24.28,
                "end": 24.54,
                "confidence": 0.619
              },
              {
                "text": "2",
                "start": 24.54,
                "end": 24.8,
                "confidence": 0.434
              },
              {
                "text": "video.",
                "start": 24.8,
                "end": 25.24,
                "confidence": 0.97
              }
            ]
          },
          {
            "id": 13,
            "start": 25.72,
            "end": 27.04,
            "text": " Which just reminds me guys,",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.956,
            "words": [
              {
                "text": "Which",
                "start": 25.72,
                "end": 26.0,
                "confidence": 0.983
              },
              {
                "text": "just",
                "start": 26.0,
                "end": 26.26,
                "confidence": 0.988
              },
              {
                "text": "reminds",
                "start": 26.26,
                "end": 26.7,
                "confidence": 0.996
              },
              {
                "text": "me",
                "start": 26.7,
                "end": 26.86,
                "confidence": 0.926
              },
              {
                "text": "guys,",
                "start": 26.86,
                "end": 27.04,
                "confidence": 0.892
              }
            ]
          },
          {
            "id": 14,
            "start": 27.06,
            "end": 28.82,
            "text": " this is part of our Columbia playlist.",
            "no_speech_prob": 0.3379374146461487,
            "confidence": 0.915,
            "words": [
              {
                "text": "this",
                "start": 27.06,
                "end": 27.26,
                "confidence": 0.982
              },
              {
                "text": "is",
                "start": 27.26,
                "end": 27.34,
                "confidence": 0.982
              },
              {
                "text": "part",
                "start": 27.34,
                "end": 27.54,
                "confidence": 0.973
              },
              {
                "text": "of",
                "start": 27.54,
                "end": 27.68,
                "confidence": 0.999
              },
              {
                "text": "our",
                "start": 27.68,
                "end": 27.82,
                "confidence": 0.991
              },
              {
                "text": "Columbia",
                "start": 27.82,
                "end": 28.24,
                "confidence": 0.997
              },
              {
                "text": "playlist.",
                "start": 28.24,
                "end": 28.82,
                "confidence": 0.58
              }
            ]
          },
          {
            "id": 15,
            "start": 28.96,
            "end": 30.36,
            "text": " I'll put it down in the description box below",
            "no_speech_prob": 0.13719242811203003,
            "confidence": 0.856,
            "words": [
              {
                "text": "I'll",
                "start": 28.96,
                "end": 29.06,
                "confidence": 0.613
              },
              {
                "text": "put",
                "start": 29.06,
                "end": 29.08,
                "confidence": 0.964
              },
              {
                "text": "it",
                "start": 29.08,
                "end": 29.2,
                "confidence": 0.993
              },
              {
                "text": "down",
                "start": 29.2,
                "end": 29.38,
                "confidence": 0.998
              },
              {
                "text": "in",
                "start": 29.38,
                "end": 29.54,
                "confidence": 0.702
              },
              {
                "text": "the",
                "start": 29.54,
                "end": 29.6,
                "confidence": 0.871
              },
              {
                "text": "description",
                "start": 29.6,
                "end": 29.86,
                "confidence": 0.999
              },
              {
                "text": "box",
                "start": 29.86,
                "end": 30.12,
                "confidence": 0.984
              },
              {
                "text": "below",
                "start": 30.12,
                "end": 30.36,
                "confidence": 0.979
              }
            ]
          },
          {
            "id": 16,
            "start": 30.44,
            "end": 32.42,
            "text": " and I'll talk about that more at the end of the video.",
            "no_speech_prob": 0.13719242811203003,
            "confidence": 0.942,
            "words": [
              {
                "text": "and",
                "start": 30.44,
                "end": 30.54,
                "confidence": 0.994
              },
              {
                "text": "I'll",
                "start": 30.54,
                "end": 30.68,
                "confidence": 0.972
              },
              {
                "text": "talk",
                "start": 30.68,
                "end": 30.82,
                "confidence": 0.994
              },
              {
                "text": "about",
                "start": 30.82,
                "end": 30.94,
                "confidence": 0.983
              },
              {
                "text": "that",
                "start": 30.94,
                "end": 31.1,
                "confidence": 0.92
              },
              {
                "text": "more",
                "start": 31.1,
                "end": 31.3,
                "confidence": 0.975
              },
              {
                "text": "at",
                "start": 31.3,
                "end": 31.52,
                "confidence": 0.589
              },
              {
                "text": "the",
                "start": 31.52,
                "end": 31.54,
                "confidence": 0.984
              },
              {
                "text": "end",
                "start": 31.54,
                "end": 31.7,
                "confidence": 0.996
              },
              {
                "text": "of",
                "start": 31.7,
                "end": 31.84,
                "confidence": 0.976
              },
              {
                "text": "the",
                "start": 31.84,
                "end": 31.94,
                "confidence": 0.991
              },
              {
                "text": "video.",
                "start": 31.94,
                "end": 32.42,
                "confidence": 0.999
              }
            ]
          },
          {
            "id": 17,
            "start": 32.72,
            "end": 33.51,
            "text": " But if you're new here,",
            "no_speech_prob": 0.13719242811203003,
            "confidence": 0.99,
            "words": [
              {
                "text": "But",
                "start": 32.72,
                "end": 32.84,
                "confidence": 0.992
              },
              {
                "text": "if",
                "start": 32.84,
                "end": 32.96,
                "confidence": 0.988
              },
              {
                "text": "you're",
                "start": 32.96,
                "end": 33.12,
                "confidence": 0.983
              },
              {
                "text": "new",
                "start": 33.12,
                "end": 33.24,
                "confidence": 0.998
              },
              {
                "text": "here,",
                "start": 33.24,
                "end": 33.51,
                "confidence": 0.994
              }
            ]
          },
          {
            "id": 18,
            "start": 33.51,
            "end": 35.78,
            "text": " join me every single Monday to learn about new countries",
            "no_speech_prob": 0.13719242811203003,
            "confidence": 0.887,
            "words": [
              {
                "text": "join",
                "start": 33.51,
                "end": 33.94,
                "confidence": 0.961
              },
              {
                "text": "me",
                "start": 33.94,
                "end": 34.08,
                "confidence": 1.0
              },
              {
                "text": "every",
                "start": 34.08,
                "end": 34.24,
                "confidence": 0.912
              },
              {
                "text": "single",
                "start": 34.24,
                "end": 34.46,
                "confidence": 0.999
              },
              {
                "text": "Monday",
                "start": 34.46,
                "end": 34.72,
                "confidence": 0.967
              },
              {
                "text": "to",
                "start": 34.72,
                "end": 34.82,
                "confidence": 0.809
              },
              {
                "text": "learn",
                "start": 34.82,
                "end": 35.02,
                "confidence": 0.99
              },
              {
                "text": "about",
                "start": 35.02,
                "end": 35.18,
                "confidence": 0.671
              },
              {
                "text": "new",
                "start": 35.18,
                "end": 35.38,
                "confidence": 0.694
              },
              {
                "text": "countries",
                "start": 35.38,
                "end": 35.78,
                "confidence": 0.949
              }
            ]
          },
          {
            "id": 19,
            "start": 35.86,
            "end": 36.38,
            "text": " from around the world.",
            "no_speech_prob": 0.13719242811203003,
            "confidence": 0.992,
            "words": [
              {
                "text": "from",
                "start": 35.86,
                "end": 35.98,
                "confidence": 0.98
              },
              {
                "text": "around",
                "start": 35.98,
                "end": 36.22,
                "confidence": 0.995
              },
              {
                "text": "the",
                "start": 36.22,
                "end": 36.36,
                "confidence": 0.994
              },
              {
                "text": "world.",
                "start": 36.36,
                "end": 36.38,
                "confidence": 0.997
              }
            ]
          },
          {
            "id": 20,
            "start": 36.38,
            "end": 37.93,
            "text": " You can do that by hitting that subscribe",
            "no_speech_prob": 0.13719242811203003,
            "confidence": 0.977,
            "words": [
              {
                "text": "You",
                "start": 36.38,
                "end": 36.6,
                "confidence": 0.982
              },
              {
                "text": "can",
                "start": 36.6,
                "end": 36.74,
                "confidence": 0.998
              },
              {
                "text": "do",
                "start": 36.74,
                "end": 36.84,
                "confidence": 0.999
              },
              {
                "text": "that",
                "start": 36.84,
                "end": 37.0,
                "confidence": 0.999
              },
              {
                "text": "by",
                "start": 37.0,
                "end": 37.16,
                "confidence": 0.96
              },
              {
                "text": "hitting",
                "start": 37.16,
                "end": 37.36,
                "confidence": 0.925
              },
              {
                "text": "that",
                "start": 37.36,
                "end": 37.5,
                "confidence": 0.994
              },
              {
                "text": "subscribe",
                "start": 37.5,
                "end": 37.93,
                "confidence": 0.962
              }
            ]
          },
          {
            "id": 21,
            "start": 37.93,
            "end": 39.32,
            "text": " and that belt notification button.",
            "no_speech_prob": 0.13719242811203003,
            "confidence": 0.909,
            "words": [
              {
                "text": "and",
                "start": 37.93,
                "end": 38.14,
                "confidence": 0.938
              },
              {
                "text": "that",
                "start": 38.14,
                "end": 38.32,
                "confidence": 0.985
              },
              {
                "text": "belt",
                "start": 38.32,
                "end": 38.48,
                "confidence": 0.706
              },
              {
                "text": "notification",
                "start": 38.48,
                "end": 39.04,
                "confidence": 0.951
              },
              {
                "text": "button.",
                "start": 39.04,
                "end": 39.32,
                "confidence": 0.999
              }
            ]
          },
          {
            "id": 22,
            "start": 39.32,
            "end": 41.24,
            "text": " But that skits.",
            "no_speech_prob": 0.13719242811203003,
            "confidence": 0.759,
            "words": [
              {
                "text": "But",
                "start": 39.32,
                "end": 40.36,
                "confidence": 0.993
              },
              {
                "text": "that",
                "start": 40.36,
                "end": 40.6,
                "confidence": 0.645
              },
              {
                "text": "skits.",
                "start": 40.6,
                "end": 41.24,
                "confidence": 0.719
              }
            ]
          }
        ]
      }
    ]


As anticipated, the returned JSON file has not only the snippets of transcribed text, but along with each includes timestamps and a "confidence" value for the accuracy of each transcription.

### Using a Non-Default Model

To use a [non-default model](../../modules/ai_modules/transcribe_module.md#available-models-in-the-transcribe-module) like [`whisper-large-v3`](https://huggingface.co/openai/whisper-large-v3), we must enter it explicitly through the [`modules`](../../system/parameters_processing_files_through_pipelines/process_method.md#selecting-models-via-the-modules-argument) argument when invoking the [`.process`](../../system/parameters_processing_files_through_pipelines/process_method.md) method.

We do so below to process the same input file shown above.


```python
# process the file with a non-default model
process_output = pipeline.process(local_file_path="../../../data/input/Interesting Facts About Colombia.mp3", # all parameters save 'modules' as above
                                  local_save_directory="../../../data/output",
                                  expire_time=60 * 30,
                                  wait_for_process=True,
                                  verbose=False,
                                  modules={"transcribe": {"model": "whisper-large-v3"}}) # specify a non-default model for this process as well as its parameters
```

We once again print out and review the output as we did above.


```python
# nicely print the output of this process
print(json.dumps(process_output, indent=2))
```

    {
      "status_code": 200,
      "pipeline": "single_transcribe_1",
      "request_id": "64729242-e15a-443f-a8f8-93e8cb66429c",
      "file_id": "692faf88-b816-4bac-951e-3034cac01b36",
      "message": "SUCCESS - output fetched for file_id 692faf88-b816-4bac-951e-3034cac01b36.Output saved to location(s) listed in process_output_files.",
      "warnings": [],
      "process_output": [
        {
          "transcript": " Episode looking at the great country of Colombia We looked at some really just basic facts its name a bit of its history the type of people that live there Landsize and all that jazz, but in this video, we're gonna go into a little bit more of a detailed look Yo, what is going on guys? Welcome back to have to D facts a channel where I look at people cultures and places My name is Dave Walpole and today we are gonna be looking more at Colombia in our Columbia part 2 video Which just reminds me guys, this is part of our Columbia playlist I'll put it down there in the description box below and I'll talk about that more at the end of the video But if you're new here join me every single Monday to learn about new countries from around the world You can do that by hitting that subscribe and that belt notification button, but let's get started",
          "timestamped_transcript": [
            {
              "id": 0,
              "start": 0.0,
              "end": 2.14,
              "text": " Episode looking at the great country of Colombia",
              "no_speech_prob": 0.08506601303815842,
              "confidence": 0.931,
              "words": [
                {
                  "text": "Episode",
                  "start": 0.0,
                  "end": 0.48,
                  "confidence": 0.706
                },
                {
                  "text": "looking",
                  "start": 0.48,
                  "end": 0.86,
                  "confidence": 0.996
                },
                {
                  "text": "at",
                  "start": 0.86,
                  "end": 1.02,
                  "confidence": 1.0
                },
                {
                  "text": "the",
                  "start": 1.02,
                  "end": 1.12,
                  "confidence": 0.999
                },
                {
                  "text": "great",
                  "start": 1.12,
                  "end": 1.34,
                  "confidence": 0.984
                },
                {
                  "text": "country",
                  "start": 1.34,
                  "end": 1.68,
                  "confidence": 0.997
                },
                {
                  "text": "of",
                  "start": 1.68,
                  "end": 1.82,
                  "confidence": 1.0
                },
                {
                  "text": "Colombia",
                  "start": 1.82,
                  "end": 2.14,
                  "confidence": 0.82
                }
              ]
            },
            {
              "id": 1,
              "start": 2.2,
              "end": 7.52,
              "text": " We looked at some really just basic facts its name a bit of its history the type of people that live there",
              "no_speech_prob": 0.08506601303815842,
              "confidence": 0.925,
              "words": [
                {
                  "text": "We",
                  "start": 2.2,
                  "end": 2.34,
                  "confidence": 0.874
                },
                {
                  "text": "looked",
                  "start": 2.34,
                  "end": 2.6,
                  "confidence": 0.999
                },
                {
                  "text": "at",
                  "start": 2.6,
                  "end": 2.78,
                  "confidence": 1.0
                },
                {
                  "text": "some",
                  "start": 2.78,
                  "end": 3.04,
                  "confidence": 0.999
                },
                {
                  "text": "really",
                  "start": 3.04,
                  "end": 3.34,
                  "confidence": 0.937
                },
                {
                  "text": "just",
                  "start": 3.34,
                  "end": 3.54,
                  "confidence": 0.996
                },
                {
                  "text": "basic",
                  "start": 3.54,
                  "end": 3.94,
                  "confidence": 0.997
                },
                {
                  "text": "facts",
                  "start": 3.94,
                  "end": 4.38,
                  "confidence": 0.941
                },
                {
                  "text": "its",
                  "start": 4.38,
                  "end": 4.58,
                  "confidence": 0.794
                },
                {
                  "text": "name",
                  "start": 4.58,
                  "end": 4.92,
                  "confidence": 0.999
                },
                {
                  "text": "a",
                  "start": 4.92,
                  "end": 5.08,
                  "confidence": 0.994
                },
                {
                  "text": "bit",
                  "start": 5.08,
                  "end": 5.22,
                  "confidence": 1.0
                },
                {
                  "text": "of",
                  "start": 5.22,
                  "end": 5.34,
                  "confidence": 1.0
                },
                {
                  "text": "its",
                  "start": 5.34,
                  "end": 5.52,
                  "confidence": 0.998
                },
                {
                  "text": "history",
                  "start": 5.52,
                  "end": 5.92,
                  "confidence": 0.999
                },
                {
                  "text": "the",
                  "start": 5.92,
                  "end": 6.38,
                  "confidence": 0.526
                },
                {
                  "text": "type",
                  "start": 6.38,
                  "end": 6.54,
                  "confidence": 0.997
                },
                {
                  "text": "of",
                  "start": 6.54,
                  "end": 6.6,
                  "confidence": 0.999
                },
                {
                  "text": "people",
                  "start": 6.6,
                  "end": 6.82,
                  "confidence": 1.0
                },
                {
                  "text": "that",
                  "start": 6.82,
                  "end": 7.0,
                  "confidence": 0.999
                },
                {
                  "text": "live",
                  "start": 7.0,
                  "end": 7.24,
                  "confidence": 0.723
                },
                {
                  "text": "there",
                  "start": 7.24,
                  "end": 7.52,
                  "confidence": 0.79
                }
              ]
            },
            {
              "id": 2,
              "start": 7.68,
              "end": 12.6,
              "text": " Landsize and all that jazz, but in this video, we're gonna go into a little bit more of a detailed look",
              "no_speech_prob": 0.08506601303815842,
              "confidence": 0.946,
              "words": [
                {
                  "text": "Landsize",
                  "start": 7.68,
                  "end": 8.28,
                  "confidence": 0.768
                },
                {
                  "text": "and",
                  "start": 8.28,
                  "end": 8.46,
                  "confidence": 0.99
                },
                {
                  "text": "all",
                  "start": 8.46,
                  "end": 8.72,
                  "confidence": 1.0
                },
                {
                  "text": "that",
                  "start": 8.72,
                  "end": 8.92,
                  "confidence": 1.0
                },
                {
                  "text": "jazz,",
                  "start": 8.92,
                  "end": 9.34,
                  "confidence": 0.992
                },
                {
                  "text": "but",
                  "start": 9.54,
                  "end": 9.62,
                  "confidence": 1.0
                },
                {
                  "text": "in",
                  "start": 9.62,
                  "end": 9.72,
                  "confidence": 1.0
                },
                {
                  "text": "this",
                  "start": 9.72,
                  "end": 9.92,
                  "confidence": 1.0
                },
                {
                  "text": "video,",
                  "start": 9.92,
                  "end": 10.1,
                  "confidence": 1.0
                },
                {
                  "text": "we're",
                  "start": 10.12,
                  "end": 10.28,
                  "confidence": 1.0
                },
                {
                  "text": "gonna",
                  "start": 10.28,
                  "end": 10.36,
                  "confidence": 0.947
                },
                {
                  "text": "go",
                  "start": 10.36,
                  "end": 10.5,
                  "confidence": 1.0
                },
                {
                  "text": "into",
                  "start": 10.5,
                  "end": 10.7,
                  "confidence": 0.998
                },
                {
                  "text": "a",
                  "start": 10.7,
                  "end": 10.9,
                  "confidence": 1.0
                },
                {
                  "text": "little",
                  "start": 10.9,
                  "end": 11.14,
                  "confidence": 0.999
                },
                {
                  "text": "bit",
                  "start": 11.14,
                  "end": 11.34,
                  "confidence": 1.0
                },
                {
                  "text": "more",
                  "start": 11.34,
                  "end": 11.6,
                  "confidence": 0.998
                },
                {
                  "text": "of",
                  "start": 11.6,
                  "end": 11.76,
                  "confidence": 0.997
                },
                {
                  "text": "a",
                  "start": 11.76,
                  "end": 11.86,
                  "confidence": 1.0
                },
                {
                  "text": "detailed",
                  "start": 11.86,
                  "end": 12.28,
                  "confidence": 0.997
                },
                {
                  "text": "look",
                  "start": 12.28,
                  "end": 12.6,
                  "confidence": 0.512
                }
              ]
            },
            {
              "id": 3,
              "start": 12.76,
              "end": 17.52,
              "text": " Yo, what is going on guys? Welcome back to have to D facts a channel where I look at people cultures and places",
              "no_speech_prob": 0.08506601303815842,
              "confidence": 0.834,
              "words": [
                {
                  "text": "Yo,",
                  "start": 12.76,
                  "end": 13.04,
                  "confidence": 0.795
                },
                {
                  "text": "what",
                  "start": 13.04,
                  "end": 13.36,
                  "confidence": 1.0
                },
                {
                  "text": "is",
                  "start": 13.36,
                  "end": 13.5,
                  "confidence": 1.0
                },
                {
                  "text": "going",
                  "start": 13.5,
                  "end": 13.72,
                  "confidence": 0.999
                },
                {
                  "text": "on",
                  "start": 13.72,
                  "end": 13.96,
                  "confidence": 0.999
                },
                {
                  "text": "guys?",
                  "start": 13.96,
                  "end": 14.32,
                  "confidence": 0.973
                },
                {
                  "text": "Welcome",
                  "start": 14.32,
                  "end": 14.58,
                  "confidence": 0.66
                },
                {
                  "text": "back",
                  "start": 14.58,
                  "end": 14.88,
                  "confidence": 0.994
                },
                {
                  "text": "to",
                  "start": 14.88,
                  "end": 15.04,
                  "confidence": 0.987
                },
                {
                  "text": "have",
                  "start": 15.04,
                  "end": 15.14,
                  "confidence": 0.382
                },
                {
                  "text": "to",
                  "start": 15.14,
                  "end": 15.26,
                  "confidence": 0.6
                },
                {
                  "text": "D",
                  "start": 15.26,
                  "end": 15.4,
                  "confidence": 0.278
                },
                {
                  "text": "facts",
                  "start": 15.4,
                  "end": 15.7,
                  "confidence": 0.91
                },
                {
                  "text": "a",
                  "start": 15.7,
                  "end": 15.84,
                  "confidence": 0.593
                },
                {
                  "text": "channel",
                  "start": 15.84,
                  "end": 16.02,
                  "confidence": 0.997
                },
                {
                  "text": "where",
                  "start": 16.02,
                  "end": 16.16,
                  "confidence": 0.977
                },
                {
                  "text": "I",
                  "start": 16.16,
                  "end": 16.22,
                  "confidence": 0.989
                },
                {
                  "text": "look",
                  "start": 16.22,
                  "end": 16.38,
                  "confidence": 0.994
                },
                {
                  "text": "at",
                  "start": 16.38,
                  "end": 16.5,
                  "confidence": 0.998
                },
                {
                  "text": "people",
                  "start": 16.5,
                  "end": 16.68,
                  "confidence": 0.998
                },
                {
                  "text": "cultures",
                  "start": 16.68,
                  "end": 17.0,
                  "confidence": 0.994
                },
                {
                  "text": "and",
                  "start": 17.0,
                  "end": 17.2,
                  "confidence": 0.948
                },
                {
                  "text": "places",
                  "start": 17.2,
                  "end": 17.52,
                  "confidence": 0.998
                }
              ]
            },
            {
              "id": 4,
              "start": 17.52,
              "end": 25.16,
              "text": " My name is Dave Walpole and today we are gonna be looking more at Colombia in our Columbia part 2 video",
              "no_speech_prob": 0.08506601303815842,
              "confidence": 0.861,
              "words": [
                {
                  "text": "My",
                  "start": 17.52,
                  "end": 17.88,
                  "confidence": 0.808
                },
                {
                  "text": "name",
                  "start": 17.88,
                  "end": 18.22,
                  "confidence": 1.0
                },
                {
                  "text": "is",
                  "start": 18.22,
                  "end": 19.04,
                  "confidence": 0.999
                },
                {
                  "text": "Dave",
                  "start": 19.04,
                  "end": 19.48,
                  "confidence": 0.956
                },
                {
                  "text": "Walpole",
                  "start": 19.48,
                  "end": 20.0,
                  "confidence": 0.892
                },
                {
                  "text": "and",
                  "start": 20.0,
                  "end": 20.36,
                  "confidence": 0.547
                },
                {
                  "text": "today",
                  "start": 20.36,
                  "end": 21.08,
                  "confidence": 0.965
                },
                {
                  "text": "we",
                  "start": 21.08,
                  "end": 21.66,
                  "confidence": 0.49
                },
                {
                  "text": "are",
                  "start": 21.66,
                  "end": 22.06,
                  "confidence": 0.996
                },
                {
                  "text": "gonna",
                  "start": 22.06,
                  "end": 22.24,
                  "confidence": 0.937
                },
                {
                  "text": "be",
                  "start": 22.24,
                  "end": 22.38,
                  "confidence": 0.999
                },
                {
                  "text": "looking",
                  "start": 22.38,
                  "end": 22.62,
                  "confidence": 0.999
                },
                {
                  "text": "more",
                  "start": 22.62,
                  "end": 23.02,
                  "confidence": 0.998
                },
                {
                  "text": "at",
                  "start": 23.02,
                  "end": 23.26,
                  "confidence": 0.999
                },
                {
                  "text": "Colombia",
                  "start": 23.26,
                  "end": 23.66,
                  "confidence": 0.594
                },
                {
                  "text": "in",
                  "start": 23.66,
                  "end": 23.86,
                  "confidence": 0.992
                },
                {
                  "text": "our",
                  "start": 23.86,
                  "end": 24.02,
                  "confidence": 0.999
                },
                {
                  "text": "Columbia",
                  "start": 24.02,
                  "end": 24.28,
                  "confidence": 0.603
                },
                {
                  "text": "part",
                  "start": 24.28,
                  "end": 24.54,
                  "confidence": 0.859
                },
                {
                  "text": "2",
                  "start": 24.54,
                  "end": 24.82,
                  "confidence": 0.821
                },
                {
                  "text": "video",
                  "start": 24.82,
                  "end": 25.16,
                  "confidence": 0.995
                }
              ]
            },
            {
              "id": 5,
              "start": 25.76,
              "end": 28.8,
              "text": " Which just reminds me guys, this is part of our Columbia playlist",
              "no_speech_prob": 0.08506601303815842,
              "confidence": 0.905,
              "words": [
                {
                  "text": "Which",
                  "start": 25.76,
                  "end": 25.96,
                  "confidence": 0.621
                },
                {
                  "text": "just",
                  "start": 25.96,
                  "end": 26.28,
                  "confidence": 1.0
                },
                {
                  "text": "reminds",
                  "start": 26.28,
                  "end": 26.72,
                  "confidence": 1.0
                },
                {
                  "text": "me",
                  "start": 26.72,
                  "end": 26.86,
                  "confidence": 0.999
                },
                {
                  "text": "guys,",
                  "start": 26.86,
                  "end": 27.08,
                  "confidence": 0.998
                },
                {
                  "text": "this",
                  "start": 27.14,
                  "end": 27.26,
                  "confidence": 1.0
                },
                {
                  "text": "is",
                  "start": 27.26,
                  "end": 27.38,
                  "confidence": 1.0
                },
                {
                  "text": "part",
                  "start": 27.38,
                  "end": 27.56,
                  "confidence": 1.0
                },
                {
                  "text": "of",
                  "start": 27.56,
                  "end": 27.66,
                  "confidence": 1.0
                },
                {
                  "text": "our",
                  "start": 27.66,
                  "end": 27.84,
                  "confidence": 1.0
                },
                {
                  "text": "Columbia",
                  "start": 27.84,
                  "end": 28.3,
                  "confidence": 0.499
                },
                {
                  "text": "playlist",
                  "start": 28.3,
                  "end": 28.8,
                  "confidence": 0.979
                }
              ]
            },
            {
              "id": 6,
              "start": 28.82,
              "end": 32.4,
              "text": " I'll put it down there in the description box below and I'll talk about that more at the end of the video",
              "no_speech_prob": 0.0007337600691244006,
              "confidence": 0.977,
              "words": [
                {
                  "text": "I'll",
                  "start": 28.82,
                  "end": 29.02,
                  "confidence": 0.952
                },
                {
                  "text": "put",
                  "start": 29.02,
                  "end": 29.1,
                  "confidence": 1.0
                },
                {
                  "text": "it",
                  "start": 29.1,
                  "end": 29.22,
                  "confidence": 0.999
                },
                {
                  "text": "down",
                  "start": 29.22,
                  "end": 29.36,
                  "confidence": 1.0
                },
                {
                  "text": "there",
                  "start": 29.36,
                  "end": 29.5,
                  "confidence": 0.674
                },
                {
                  "text": "in",
                  "start": 29.5,
                  "end": 29.56,
                  "confidence": 0.995
                },
                {
                  "text": "the",
                  "start": 29.56,
                  "end": 29.66,
                  "confidence": 1.0
                },
                {
                  "text": "description",
                  "start": 29.66,
                  "end": 29.9,
                  "confidence": 0.998
                },
                {
                  "text": "box",
                  "start": 29.9,
                  "end": 30.16,
                  "confidence": 0.997
                },
                {
                  "text": "below",
                  "start": 30.16,
                  "end": 30.4,
                  "confidence": 0.999
                },
                {
                  "text": "and",
                  "start": 30.4,
                  "end": 30.54,
                  "confidence": 0.991
                },
                {
                  "text": "I'll",
                  "start": 30.54,
                  "end": 30.68,
                  "confidence": 0.993
                },
                {
                  "text": "talk",
                  "start": 30.68,
                  "end": 30.82,
                  "confidence": 0.999
                },
                {
                  "text": "about",
                  "start": 30.82,
                  "end": 30.98,
                  "confidence": 0.999
                },
                {
                  "text": "that",
                  "start": 30.98,
                  "end": 31.14,
                  "confidence": 0.999
                },
                {
                  "text": "more",
                  "start": 31.14,
                  "end": 31.3,
                  "confidence": 0.994
                },
                {
                  "text": "at",
                  "start": 31.3,
                  "end": 31.44,
                  "confidence": 0.997
                },
                {
                  "text": "the",
                  "start": 31.44,
                  "end": 31.56,
                  "confidence": 1.0
                },
                {
                  "text": "end",
                  "start": 31.56,
                  "end": 31.72,
                  "confidence": 0.995
                },
                {
                  "text": "of",
                  "start": 31.72,
                  "end": 31.84,
                  "confidence": 0.992
                },
                {
                  "text": "the",
                  "start": 31.84,
                  "end": 31.98,
                  "confidence": 0.999
                },
                {
                  "text": "video",
                  "start": 31.98,
                  "end": 32.4,
                  "confidence": 0.999
                }
              ]
            },
            {
              "id": 7,
              "start": 32.7,
              "end": 36.49,
              "text": " But if you're new here join me every single Monday to learn about new countries from around the world",
              "no_speech_prob": 0.0007337600691244006,
              "confidence": 0.983,
              "words": [
                {
                  "text": "But",
                  "start": 32.7,
                  "end": 32.86,
                  "confidence": 0.943
                },
                {
                  "text": "if",
                  "start": 32.86,
                  "end": 32.96,
                  "confidence": 1.0
                },
                {
                  "text": "you're",
                  "start": 32.96,
                  "end": 33.14,
                  "confidence": 0.97
                },
                {
                  "text": "new",
                  "start": 33.14,
                  "end": 33.26,
                  "confidence": 1.0
                },
                {
                  "text": "here",
                  "start": 33.26,
                  "end": 33.56,
                  "confidence": 0.999
                },
                {
                  "text": "join",
                  "start": 33.56,
                  "end": 33.9,
                  "confidence": 0.828
                },
                {
                  "text": "me",
                  "start": 33.9,
                  "end": 34.06,
                  "confidence": 0.993
                },
                {
                  "text": "every",
                  "start": 34.06,
                  "end": 34.26,
                  "confidence": 0.987
                },
                {
                  "text": "single",
                  "start": 34.26,
                  "end": 34.5,
                  "confidence": 1.0
                },
                {
                  "text": "Monday",
                  "start": 34.5,
                  "end": 34.72,
                  "confidence": 0.995
                },
                {
                  "text": "to",
                  "start": 34.72,
                  "end": 34.88,
                  "confidence": 1.0
                },
                {
                  "text": "learn",
                  "start": 34.88,
                  "end": 35.02,
                  "confidence": 1.0
                },
                {
                  "text": "about",
                  "start": 35.02,
                  "end": 35.2,
                  "confidence": 0.999
                },
                {
                  "text": "new",
                  "start": 35.2,
                  "end": 35.44,
                  "confidence": 0.998
                },
                {
                  "text": "countries",
                  "start": 35.44,
                  "end": 35.78,
                  "confidence": 0.995
                },
                {
                  "text": "from",
                  "start": 35.78,
                  "end": 36.0,
                  "confidence": 0.996
                },
                {
                  "text": "around",
                  "start": 36.0,
                  "end": 36.22,
                  "confidence": 0.999
                },
                {
                  "text": "the",
                  "start": 36.22,
                  "end": 36.36,
                  "confidence": 0.999
                },
                {
                  "text": "world",
                  "start": 36.36,
                  "end": 36.49,
                  "confidence": 0.999
                }
              ]
            },
            {
              "id": 8,
              "start": 36.49,
              "end": 41.48,
              "text": " You can do that by hitting that subscribe and that belt notification button, but let's get started",
              "no_speech_prob": 0.0007337600691244006,
              "confidence": 0.923,
              "words": [
                {
                  "text": "You",
                  "start": 36.49,
                  "end": 36.62,
                  "confidence": 0.705
                },
                {
                  "text": "can",
                  "start": 36.62,
                  "end": 36.72,
                  "confidence": 1.0
                },
                {
                  "text": "do",
                  "start": 36.72,
                  "end": 36.86,
                  "confidence": 1.0
                },
                {
                  "text": "that",
                  "start": 36.86,
                  "end": 37.02,
                  "confidence": 1.0
                },
                {
                  "text": "by",
                  "start": 37.02,
                  "end": 37.18,
                  "confidence": 0.999
                },
                {
                  "text": "hitting",
                  "start": 37.18,
                  "end": 37.36,
                  "confidence": 0.993
                },
                {
                  "text": "that",
                  "start": 37.36,
                  "end": 37.54,
                  "confidence": 0.998
                },
                {
                  "text": "subscribe",
                  "start": 37.54,
                  "end": 37.92,
                  "confidence": 0.994
                },
                {
                  "text": "and",
                  "start": 37.92,
                  "end": 38.14,
                  "confidence": 0.812
                },
                {
                  "text": "that",
                  "start": 38.14,
                  "end": 38.32,
                  "confidence": 0.99
                },
                {
                  "text": "belt",
                  "start": 38.32,
                  "end": 38.52,
                  "confidence": 0.792
                },
                {
                  "text": "notification",
                  "start": 38.52,
                  "end": 39.12,
                  "confidence": 0.989
                },
                {
                  "text": "button,",
                  "start": 39.12,
                  "end": 39.5,
                  "confidence": 0.996
                },
                {
                  "text": "but",
                  "start": 39.7,
                  "end": 40.24,
                  "confidence": 1.0
                },
                {
                  "text": "let's",
                  "start": 40.24,
                  "end": 40.94,
                  "confidence": 0.752
                },
                {
                  "text": "get",
                  "start": 40.94,
                  "end": 41.22,
                  "confidence": 0.988
                },
                {
                  "text": "started",
                  "start": 41.22,
                  "end": 41.48,
                  "confidence": 0.972
                }
              ]
            }
          ]
        }
      ],
      "process_output_files": [
        "../../../data/output/692faf88-b816-4bac-951e-3034cac01b36.json"
      ]
    }
