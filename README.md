# Project Overview  
This project focuses on building a chatbot, **MediGuide**, capable of assisting users with symptom-based guidance. The chatbot leverages natural language processing (NLP) and machine learning techniques to understand user inputs and respond accurately based on predefined intents. It is designed to provide a conversational interface for users to interact with the system seamlessly.  

## Data Source  
The initial dataset for this project was obtained from [Kaggle](https://www.kaggle.com), and it was customized to suit the requirements of the chatbot. The dataset is stored in a JSON file (`symptoms_Intent1.json`) and contains predefined intents, patterns (user inputs), and corresponding responses.  

## Implementation Details  

### Data Preparation  
1. **Data Loading**:  
   - The JSON file is loaded, and intents are parsed to extract `patterns` (user queries) and `tags` (associated categories).  
   - Each tag is mapped to a set of possible responses for the chatbot.  

2. **Label Encoding**:  
   - Tags are encoded into numerical format using `LabelEncoder` to prepare them for model training.  

3. **Text Tokenization and Padding**:  
   - Tokenized the user queries into sequences of integers using the `Tokenizer` class.  
   - Applied padding to ensure uniform sequence length (`max_len`), accommodating input length variations.  

### Model Development  
1. **Architecture**:  
   - A sequential neural network with the following layers:  
     - **Embedding Layer**: Converts text tokens into dense vectors of fixed size.  
     - **GlobalAveragePooling1D Layer**: Reduces dimensionality by averaging over the sequence length.  
     - **Dense Layers**: Two hidden layers with ReLU activation for learning features.  
     - **Output Layer**: Softmax activation to classify inputs into multiple categories (tags).  

2. **Compilation**:  
   - Optimized using the Adam optimizer.  
   - Loss function: `sparse_categorical_crossentropy` for multi-class classification.  

3. **Training**:  
   - Trained for 500 epochs using padded input sequences and encoded labels.  
   - Achieved high accuracy on the training data.  

4. **Saving the Model**:  
   - Stored the trained model as `chat_model`.  
   - Saved the tokenizer and label encoder objects using `pickle` for later use.  

### Chatbot Interaction (`chat()`)  
1. **Loading Components**:  
   - Loads the saved model, tokenizer, and label encoder for real-time inference.  

2. **User Input Processing**:  
   - Accepts user queries, tokenizes and pads them to match the training input format.  

3. **Response Generation**:  
   - Predicts the intent tag for the input query using the trained model.  
   - Selects a random response associated with the predicted tag from the JSON file.  

4. **Interactive Features**:  
   - Provides a conversational experience where users can type their symptoms and receive helpful responses.  
   - Includes a command to exit the chat by typing `quit`.  

## Results and Evaluation  
The chatbot provides accurate responses based on trained intents and patterns, offering a functional and user-friendly conversational experience. Its modular design allows easy customization to expand intents and responses, making it versatile for various domains.  
