# questions
Developed an AI to answer questions.

HOW TO RUN THIS :
                  Run using command "python3 questions.py corpus"
                  Then it asks for a query as input after we giving query it prints out best answer found.

BREIF DESCRIPTION : 
    Question Answering (QA) is a field within natural language processing focused on designing systems that can answer questions.
    
    Our question answering system will perform two tasks: document retrieval and passage retrieval.
    Our system will have access to a corpus of text documents.
    When presented with a query (a question in English asked by the user), document retrieval will first identify which document(s) are most relevant to the query.
    Once the top documents are found, the top document(s) will be subdivided into passages (in this case, sentences) so that the most relevant passage to the question can be determined.
    To find the most relevant documents, we’ll use tf-idf to rank documents based both on term frequency for words in the query as well as inverse document frequency for words in the query. 
    Once we’ve found the most relevant documents, there many possible metrics for scoring passages, but we’ll use a combination of inverse document frequency and a query term density measure (described in the Specification).
    
    
UNDERSTANDING CODE : 

    First, take a look at the documents in corpus. Each is a text file containing the contents of a Wikipedia page.
    Our goal is to write an AI that can find sentences from these files that are relevant to a user’s query. 
    You are welcome and encouraged to add, remove, or modify files in the corpus if you’d like to experiment with answering queries based on a different corpus of documents.
    Just be sure each file in the corpus is a text file ending in .txt.
    
    Now, take a look at questions.py. The global variable FILE_MATCHES specifies how many files should be matched for any given query.
    The global variable SENTENCES_MATCHES specifies how many sentences within those files should be matched for any given query.
    By default, each of these values is 1: our AI will find the top sentence from the top matching document as the answer to our question.
    You are welcome and encouraged to experiment with changing these values.
    
    In the main function, we first load the files from the corpus directory into memory (via the load_files function). 
    Each of the files is then tokenized (via tokenize) into a list of words, which then allows us to compute inverse document frequency values for each of the words (via compute_idfs).
    The user is then prompted to enter a query. The top_files function identifies the files that are the best match for the query.
    From those files, sentences are extracted, and the top_sentences function identifies the sentences that are the best match for the query.
    
    
IMPLEMENTATION OF load_files FUNCTION : 
    The load_files function accepts the name of a directory and return a dictionary mapping the filename of each .txt file inside that directory to the file’s contents as a string.
    
IMPLEMENTATION OF tokenize FUNCTION :
    The tokenize function accepts a document (a string) as input, and return a list of all of the words in that document, in order and lowercased.
    I used nltk’s word_tokenize function to perform tokenization. Filter out punctuation and stopwords.
    
IMPLEMENTATION OF compute_idfs FUNCTION :
    The compute_idfs function should accept a dictionary of documents and return a new dictionary mapping words to their IDF (inverse document frequency) values.
    Documents will be a dictionary mapping names of documents to a list of words in that document.
    The returned dictionary should map every word that appears in at least one of the documents to its inverse document frequency value.
    The inverse document frequency of a word is defined by taking the natural logarithm of the number of documents divided by the number of documents in which the word appears.
    
IMPLEMENTATION OF top_files FUNCTION : 
    The top_files function should, given a query (a set of words), files (a dictionary mapping names of files to a list of their words),
    and idfs (a dictionary mapping words to their IDF values), return a list of the filenames of the the n top files that match the query,ranked according to tf-idf.
    The returned list of filenames should be of length n and should be ordered with the best match first.
    Files should be ranked according to the sum of tf-idf values for any word in the query that also appears in the file. 
    Words in the query that do not appear in the file should not contribute to the file’s score.
    
IMPLEMENTATION OF top_sentences FUNCTION : 
    The top_sentences function should, given a query (a set of words), sentences (a dictionary mapping sentences to a list of their words), and idfs (a dictionary mapping words to their IDF values), return a list of the n top sentences that match the query, ranked according to IDF.
    The returned list of sentences should be of length n and should be ordered with the best match first.
    Sentences should be ranked according to “matching word measure”: namely, the sum of IDF values for any word in the query that also appears in the sentence. Note that term frequency should not be taken into account here, only inverse document frequency.
    If two sentences have the same value according to the matching word measure, then sentences with a higher “query term density” should be preferred. Query term density is defined as the proportion of words in the sentence that are also words in the query. For example, if a sentence has 10 words, 3 of which are in the query, then the sentence’s query term density is 0.3.
    
    
    
     
