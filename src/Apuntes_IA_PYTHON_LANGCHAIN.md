# Apuntes LangChain

---

## LangChain Master Class For Beginners 2024 [+20 Examples, LangChain V0.2]

https://www.youtube.com/watch?v=yF9kGESAi3M


Ejemplo chat conversacional

~~~

model = ChatOpenAI(model="gpt-4o")

chat_history = []


while True:
    query= input("tu")
    if query.lower() == "exit":
        break:
    chat_history.append(HummanMessage(content=query))

    result = model.invoke(chat_history)
    response = result.content
    chat_history.append(AIMessage(content=response))

    print("AI: {resoibse}")

print("------- Message History --------")

print(chat_history)


~~~


Ejemplos prompt template

Template string
~~~
from langchain.prompts import ChatPromptTemplate
from langchain_core.messages import HumanMessage

template = "Tell me a joke about {topic}"
prompt_template = ChatPromptTemplate.from_template(template)

print("----- Prompt from Template ------")
prompt = prompt_template.invoke("topic": "cats")
print(prompt)

~~~
Prompt with multiple placeholders

~~~

template_multiple = """you are helpful assistant.
Human: Tell me a {adjective} story about a {animal}.
Assistant:"""
promp_multiple = ChatPromptTemplate.template(template_nultiple)
prompt = promp_multiple.invoke({"adjetive": "funne","animal": "panda"})
print(prompt)


~~~

Prompt with System an Human Messages (using Tuyples)

~~~


messages = [
    ("sustem","you are a comedian who tells jokes about {topic}"),
    ("human","Tell me {joke_count} jokes"),

]
prompt_template = ChatPromptTemplate.from_messages(messages)
prompt = prompt_template.invoke("topic": "lawyers","joke_count": 3)

print(prompt)

~~~

Otra manera de meter templates:

~~~

messages = [
    ("System": "You are a comedian who tells jokes about {topic}"),
    HumanMessage(content="Tell me 3 jokes"),

]

# en humman 
prompt_template = ChatPromptTemplate.from_messages(messages)
prompt = prompt_template.invoke("topic": "lawyers","joke_count": 3)

print(prompt)

~~~



~~~


~~~




---
## LANGCHAIN 🤯 Chateando con un PDF

https://www.youtube.com/watch?v=OW6hAuAsor0




---
## Mastering Prompt Engineering for LangChain, LangGraph, and AI Agent Applications

https://becomingahacker.org/mastering-prompt-engineering-for-langchain-langgraph-and-ai-agent-applications-e26d85a55f13


---
## LangChain Prompt Templates — Teaching LLMs to Talk Your Way

https://blog.gopenai.com/langchain-prompt-templates-teaching-llms-to-talk-your-way-6f3749da27cf




---


---



---



---
