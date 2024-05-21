## Currently Available Modules

What follows is a list of all modules currently available to [build](../system/pipeline_creation/create_pipeline.md) Krixik pipelines with. As you review the list and begin to ideate pipeline possibilities, keep in mind that (as long as outputs and inputs [match](../system/convenience_methods/convenience_methods.md)) there are no restrictions on how you can put these together. Repetition, even serial repetition, is permitted.

Given that the list of Krixik modules—and of the models within them—will constantly grow, we suggest that you bookmark this page.

### AI Model Modules

- [Image Caption](ai_model_modules/caption_module.md): Generates a textual caption for an input image.

- [OCR (Optical Character Recognition)](ai_model_modules/ocr_module.md): Extracts text from an input image.

- [Sentiment Analysis](ai_model_modules/sentiment_module.md): Performs sentiment analysis on input snippets of text (i.e. is the text positive/negative/neutral?). 

- [Summarize](ai_model_modules/summarize_module.md): Summarizes input text. 

- [Text Embedder](ai_model_modules/text-embedder_module.md): Converts input text into numerical vectors. These can then be stored in a Vector database to enable [`.semantic_search`](../system/search_methods/semantic_search_method.md).

- [Parser](ai_model_modules/parser_module.md): Divides input text files into (potentially overlapping) snippets in a JSON file.

- [Transcribe](ai_model_modules/transcribe_module.md): Transcribes an audio file's contents into text.

- [Translate](ai_model_modules/translate_module.md): Translates input text into another language.

### Database Modules

- [Vector database](database_modules/vector-db_module.md): Creates a vector database with set of input vectors. Enables [`.semantic_search`](../system/search_methods/semantic_search_method.md).

- [Keyword database](database_modules/keyword-db_module.md): Creates a relational database of keywords drawn from an input text file. Enables [`.keyword_search`](../system/search_methods/keyword_search_method.md).

### Support Function Modules

- [JSON-to-TXT](support_function_modules/json-to-txt_module.md): Converts an input JSON file to a TXT file.
