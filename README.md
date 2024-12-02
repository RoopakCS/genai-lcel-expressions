## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:
Develop an LCEL-based application to process expressions with dynamic parameters, leveraging a prompt template for structured interaction, a language model to process the input, and an output parser for extracting meaningful results.

### DESIGN STEPS:

#### STEP 1:
Create a prompt template with placeholders for at least two parameters.
#### STEP 2:
Use LangChain's language model to process the prompt and generate a response.
#### STEP 3:
Implement an output parser to extract structured results from the model's response.

### PROGRAM:
```python
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain
from langchain.chat_models import ChatOpenAI
from langchain.output_parsers import ResponseSchema
from langchain.schema.output_parser import StrOutputParser

# Define the PromptTemplate
prompt = PromptTemplate(
    template="""
You are a travel assistant. Based on the following inputs, recommend a destination:
- Preferred activity: {activity}
- Budget (in USD): {budget}

Provide a response strictly in JSON format:
{{
    "destination": "<destination>",
    "activity": "<activity>",
    "cost": "<cost>"
}}
""",
    input_variables=["activity", "budget"],
)

# Define the Output Parser
response_schemas = [
    ResponseSchema(name="destination", description="Recommended travel destination"),
    ResponseSchema(name="activity", description="Suggested activity at the destination"),
    ResponseSchema(name="cost", description="Estimated cost in USD for the trip"),
]
output_parser = StrOutputParser()

# Initialize the LLM
llm = ChatOpenAI(model="gpt-4-0613", temperature=0)

# Create the LangChain Expression (LLM Chain)
chain = LLMChain(llm=llm, prompt=prompt, output_parser=output_parser)

# Test the chain with an example
input_data = {"activity": "hiking", "budget": 1000}
result = chain.run(input_data)

# Parse the structured output
parsed_result = output_parser.parse(result)

# Display the result
print("Recommendation:", parsed_result)
```

### OUTPUT:
![alt text](Output.png)

### RESULT:
Hence,the program to design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios is written and successfully executed.
