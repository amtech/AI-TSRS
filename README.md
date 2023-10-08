# TSRS( Technical Standard Review System)
This is developed for NASA Space Apps Challenge 2023 for STAR Revolutionizing Technical Standards with AI. This is developed based on privateGPT(https://github.com/imartinez/privateGPT.git) which is a tool to ask questions about your documents without an internet connection, using the power of LLM. Here, the documents can be ingested and the model can be trained on them to answer the queries of the user. Here user has two options, one is through chat with the model second is uploading the pdf document which can be used by the mission designer to update the process document and know if there is any deviation from the standard process. This tool has the potential to reduce the time taken to detect the error as well as gain knowledge on various standard processes.

===> The following link to the Google collab can be used to develop the model and improve it by uploading more NASA Technical Standard documents from other resources. The link is https://colab.research.google.com/drive/1GhSfCqjXhbrpzH1OAqona0X3xFhG-dxQ?usp=sharing	

Environment Setup for Google Colab
In order to set your environment up to run the code here, first install all requirements:

``!pip install -r requirements.txt``

``%cd privateGPT``

```!pip install poetry```


Then, download the LLM model and place it in the models directory in privateGPT folder
- LLM: default to [ggml-gpt4all-j-v1.3-groovy.bin](https://gpt4all.io/models/ggml-gpt4all-j-v1.3-groovy.bin)

Copy the `example.env` template into `.env`

``cp example.env .env``


and edit the variables appropriately in the `.env` file.
```
MODEL_TYPE: supports LlamaCpp or GPT4All
PERSIST_DIRECTORY: is the folder you want your vectorstore in
MODEL_PATH: Path to your GPT4All or LlamaCpp supported LLM
MODEL_N_CTX: Maximum token limit for the LLM model
MODEL_N_BATCH: Number of tokens in the prompt that are fed into the model at a time. The optimal value differs a lot depending on the model (8 works well for GPT4All, and 1024 is better for LlamaCpp)
EMBEDDINGS_MODEL_NAME: SentenceTransformers embeddings model name (see https://www.sbert.net/docs/pretrained_models.html)
TARGET_SOURCE_CHUNKS: The amount of chunks (sources) that will be used to answer a question
```

Note: because of the way `langchain` loads the `SentenceTransformers` embeddings, the first time you run the script it will require internet connection to download the embeddings model itself.

## Test dataset
This repo is based on all the pdfs from NASA Technical Standards(https://standards.nasa.gov/all-standards), code to fetch them in source_documents is added in the above google colab notebook.

## Instructions for ingesting your own dataset

Put any and all your files into the `source_documents` directory

The supported extensions are:

   - `.csv`: CSV,
   - `.docx`: Word Document,
   - `.doc`: Word Document,
   - `.enex`: EverNote,
   - `.eml`: Email,
   - `.epub`: EPub,
   - `.html`: HTML File,
   - `.md`: Markdown,
   - `.msg`: Outlook Message,
   - `.odt`: Open Document Text,
   - `.pdf`: Portable Document Format (PDF),
   - `.pptx` : PowerPoint Document,
   - `.ppt` : PowerPoint Document,
   - `.txt`: Text file (UTF-8),

Run the following command to ingest all the data.

``run ingest.py``

It will create a `db` folder containing the local vectorstore. 


## Ask your Query
``run privateGPT.py``

Here, you can either ask the questions from the model using the following input.

```plaintext
> Enter a query:
```
else, you can upload the pdf in query folder, if a pdf is given there then, the code will not ask the chat query and first the pdf will be processed.

Type `exit` to finish the script.



# Disclaimer
This is for NASA Space Apps Challenge 2023 for STAR Revolutionizing Technical Standards with AI challenge based on privateGPT.
