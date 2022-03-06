# Collection-Index-Construction
Objective: Construct a searchable index for a document collection.

Key Features: The collection index is based on the inverted file structure. It has the following two components:
1. Dictionary term file.  This file contains all the index terms, their collection 
frequency (i.e., how many times this term appears in the whole collection), and a pointer 
to their corresponding posting information in the posting file.
2. Posting file.  This file contains the corresponding pointer that links entries in 
the dictionary term file to that in the posting file.  This file also includes a  repeated set of 
information that indicates the document id that the term is in,  the term frequency  (i.e., 
how many times this term appears in this document).


This Project is divided into 2 tasks and the HW2Main  class is the main class for running these tasks.:
Task 1: Build an index
Below are class descriptions used for this task:
    1. Indexing. PreProcessedCorpusReader: This class access the result.trectext and result.trecweb, and return 
       documents one by one through the next document(). 
      (Note: This class uses the result of the project - "Document Collection Processing". This project is also 
       available under project section)
   2. Indexing.MyIndexWriter: This class has one essential method IndexADocument (String docno, String content) 
       to create an index for a document represented by the docno and the content. The content is a list of words, 
       segmented by blank space. The code here is written in a very efficient way so that the memory can support it, 
       otherwise, the memory may fail to support the code.  I have constructed the index by installments, where 
      each installment works on only a block of the documents to be indexed. When processing the documents in a 
      block, everything about the index can be stored in the memory, then when all the documents in the block 
      are processed, the corresponding dictionary and postings can be stored as separate files on the hard drive so 
      that the memory is cleared for the next block of documents. Once all the blocks have been processed, there 
      will be a fusion process to merge all the dictionary files and all the posting files. The data structure used for this 
      task is "Dictionary".

Task 2: Retrieve posting lists of tokens from an index
Below are class descriptions used for this task:
    1. Indexing. MyIndexReader: This class has the following methods:
       1.MyIndexReader():  Read the index file you generated in task  1. I have not loaded the whole index into the 
         memory. First, the dictionary term file is loaded.  Once the corresponding links of the posting information of 
         the query terms are known, I loaded the relevant parts of the postings into the memory.
       2. int GetDocid( String docno ) and String getDocno( int docid ): It provides transformation between string 
           docnos and integer docids.
      3. int[][]  GetPostingList(  String token  ):  It retrieve the posting list of  the  token as a  2-dimension array
      4. int GetDocFreq( String token ): get the document frequency of the token.
      5. Long GetCollectionFreq( String token ): get the collection frequency of the token.
