# GPT-Verse 🎩 -- Library under construction

<p align="center">
  <img src="images\logo\GPT-verse.png" alt="Scrapegraph-ai Logo" style="width: 35%;">
</p>

The GPT-Verse library, is an innovative Python package designed for developers and enthusiasts working in the realm of natural language processing and generative pre-trained transformer models. With its dependency specified for Python 3.12, GPT-Verse ensures compatibility with the latest features and improvements of the Python programming language, ensuring users can leverage the most current language benefits.


## 💪 Features

- Language Generation: The GPT model excels at generating coherent and contextually relevant text based on input prompts. Users can expect GPT-Verse to provide APIs that allow them to generate text for a variety of applications, ranging from automated content creation to chatbots.

- Fine-tuning on Custom Datasets: A critical feature of GPT models is their ability to be fine-tuned on specific datasets. This allows the model to perform well on niche tasks or understand specific domains much better. GPT-Verse is likely to offer facilities to enable this fine-tuning, making it versatile for specialized applications.

- Language Understanding: Beyond generating text, GPT models are capable of understanding and parsing input text to perform tasks like sentiment analysis, summarization, and question answering. GPT-Verse may include functionalities that harness this capability, offering users tools for extracting insights from text or improving interaction with machine learning systems.

- Integration Ready: Given the nature of such libraries, GPT-Verse might be designed with integration in mind, facilitating its use alongside other Python libraries and frameworks in larger applications or systems.

## 💻 Installation

GPT-Verse requires Python 3.12 or later. It is recommended to use a virtual environment to manage the project dependencies.

To install GPT-Verse and its dependencies, follow these steps:

```bash
# Install the library from pipy
pip install gpt_verse==<last-code-version>
```

## ⚒️ Usage

1. **Use Langchain Agents as Tool**

   To start indexing your documents, you need to prepare your documents in the supported formats (PDF, PPTX, XLSX, web pages, YouTube videos).

   Example for indexing PDFs:

   ```python
   # Initialize your embeddings model
   from langchain_openai import ChatOpenAI
   from langchain_community.tools.tavily_search import TavilySearchResults
   from gpt_verse.personas import SecondPersona, FirstPersona

   llm = ChatOpenAI(
      model="gpt-4-turbo",
      max_tokens=4096 
      )

   tavily_tool = TavilySearchResults()

   # Define the second agent (it will be the contact-center)
   agent = FirstPersona(
      llm=llm,
      tools=[TavilySearchResults()],
      prompt="Help me with my task"
   )

   seconda_persona = SecondPersona(
      agent=agent.as_executor(),
      name="Mario",
      scope="search a job online",
      instructions="give detailed instruction"  # instruction will be given from the prima persona to the second persona
   )

   # Define the first agent (it will be the one to pass you to the contact-center agent)
   prima_persona = FirstPersona(
      llm=llm,
      tools=[seconda_persona.as_tool()],
      prompt="Help me with my task" # main scope of the agent
   )

   result = prima_persona.as_executor().invoke({"input": "can u help me find a job in python coding?"})
   ```

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or pull request if you have suggestions or improvements.

## 📜 License

Miner AI Beta is licensed under the MIT License. See the [MIT](LICENSE) file for more information.

## Acknowledgements

- We would like to thank all the contributors to the project and the open-source community for their support.
- GPT-Verse is meant to be used for ai data mining over documents and research purposes only. We are not responsible for any misuse of the library.