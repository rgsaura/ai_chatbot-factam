# GPT-4 & LangChain - Create a ChatGPT Chatbot for Your PDF Docs

Use the new GPT-4 api to build a chatGPT chatbot for Large PDF docs.

**If you run into errors, please review the troubleshooting section further down this page.**

## Development

1. Clone the repo

```
git clone [github https url]
```

2. Install packages

```
pnpm install
```

3. Set up your `.env` file

- Copy `.env.example` into `.env`
  Your `.env` file should look like this:

```
OPENAI_API_KEY=

PINECONE_API_KEY=
PINECONE_ENVIRONMENT=

PINECONE_INDEX_NAME=

```

- Visit [openai](https://help.openai.com/en/articles/4936850-where-do-i-find-my-secret-api-key) to retrieve API keys and insert into your `.env` file.
- Visit [pinecone](https://pinecone.io/) to create and retrieve your API keys, and also retrieve your environment and index name from the dashboard.

4. In the `config` folder, replace the `PINECONE_NAME_SPACE` with a `namespace` where you'd like to store your embeddings on Pinecone when you run `pnpm run ingest`. This namespace will later be used for queries and retrieval.

5. In `utils/makechain.ts` chain change the `QA_PROMPT` for your own usecase. Change `modelName` in `new OpenAIChat` to `gpt-3.5-turbo`, if you don't have access to `gpt-4`. Please verify outside this repo that you have access to `gpt-4`, otherwise the application will not work with it.

## Convert your PDF to embeddings

1. In `docs` folder replace the pdf with your own pdf doc.

2. In `scripts/ingest-data.ts` replace `filePath` with `docs/{yourdocname}.pdf`

3. Run the script `pnpm run ingest` to 'ingest' and embed your docs

4. Check Pinecone dashboard to verify your namespace and vectors have been added.

## Run the app

Once you've verified that the embeddings and content have been successfully added to your Pinecone, you can run the app `pnpm run dev` to launch the local dev environment, and then type a question in the chat interface.

## Troubleshooting

In general, keep an eye out in the `issues` and `discussions` section of this repo for solutions.

**General errors**

- Make sure you're running the latest Node version. Run `node -v`
- Make sure you're using the same versions of LangChain and Pinecone as this repo.
- Check that you've created an `.env` file that contains your valid (and working) API keys, environment and index name.
- If you change `modelName` in `OpenAIChat` note that the correct name of the alternative model is `gpt-3.5-turbo`
- Make sure you have access to `gpt-4` if you decide to use. Test your openAI keys outside the repo and make sure it works and that you have enough API credits.

**Pinecone errors**

- Make sure your pinecone dashboard `environment` and `index` matches the one in the `pinecone.ts` and `.env` files.
- Check that you've set the vector dimensions to `1536`.
- Make sure your pinecone namespace is in lowercase.
- Pinecone indexes of users on the Starter(free) plan are deleted after 7 days of inactivity. To prevent this, send an API request to Pinecone to reset the counter.
- Retry with a new Pinecone index.

If you're stuck after trying all these steps, delete `node_modules`, restart your computer, then `pnpm install` again.

## Credit

Frontend of this repo is inspired by [langchain-chat-nextjs](https://github.com/zahidkhawaja/langchain-chat-nextjs)
=======
