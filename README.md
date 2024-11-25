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
from langchain.llms import OpenAI
from langchain.output_parsers import StructuredOutputParser, ResponseSchema

# Define the prompt template with two parameters
prompt = PromptTemplate(
    input_variables=["topic", "context"],
    template="Write a summary about {topic} based on the following context: {context}"
)

# Initialize the language model
llm = OpenAI(model="text-davinci-003", temperature=0.7)

# Define the response schema for the output parser
response_schemas = [
    ResponseSchema(name="summary", description="A concise summary of the topic"),
    ResponseSchema(name="key_points", description="Main points covered in the summary")
]

output_parser = StructuredOutputParser.from_response_schemas(response_schemas)

# Example function to evaluate the LCEL expression
def evaluate_expression(topic, context):
    # Generate the prompt with input parameters
    formatted_prompt = prompt.format(topic=topic, context=context)
    
    # Get the response from the LLM
    raw_output = llm(formatted_prompt)
    
    # Parse the output into a structured format
    parsed_output = output_parser.parse(raw_output)
    
    return parsed_output

# Example usage
if __name__ == "__main__":
    topic = "Artificial Intelligence"
    context = "Artificial Intelligence is a field of study focusing on creating machines capable of mimicking human intelligence. It includes machine learning, robotics, and natural language processing."
    result = evaluate_expression(topic, context)
    print("LCEL Expression Output:")
    print(result)
```

### OUTPUT:
![alt text](Image.png)

### RESULT:
Hence,the program to design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios is written and successfully executed.
