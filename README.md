# NLP-Medical-Note-Explainer-MNE-
Explain medical note to people with out any such background using state-of-art summarization techniques


Doctors write notes in language and writing that is hard to understand. The ineligible writing can be mitigated by preparing elec- tronic records or computer vision algorithms that converts it to a more readable format. One other problems remains, how do ordinary peo- ple understand the medical note, even after be- ing able to read it. The main motivation behind this project is to make a note more readable. I use wikipedia API to infuse more information into the medical note and then summarizing this expanded note using state-of-the-art pre- trained models using both Abstractive and ex- tractive techniques. The results however were not satisfactory, I found a decrease in reading scores by 8.3, although my initial hypothesis was that the such a technique would increase ease of reading.

# Generating summaries
I used the Open NMT (Gehrmann et al., 2018) pre-trained models and software they provide to summarize text. I used a pre-trained model as given the lack of superivised training data it was not possible to train the model my- self. They also provide several different mod- els to test on. (https://opennmt.net/OpenNMT py/Summarization.html)

# Embedding definitions from Wikipedia
For each token in the inference portion, I fetch the wikipedia definition (upto 3 sentences) and add it to the note. This expands the note and adds more information to it that can be understood by the or- dinary reader. But this expanded note is too ver- bose.

# Sliding window
One of my first tasks is to clean the data. This involves focusing on the most important hard to understand parts in the note. As mentioned above, a note in my data set contains 3 different portions and I am working with the 3rd hard inference por- tion. The way I detect the hardest to infer por- tion is to create a small script that iterates over the entire text of a note (prior to embedding with Wikipedia information). It selects the index of the token which had the least readibility scores, given the window. From this index onwards would form the portion of the note I would infer. With manual inspection, I found that this technique worked well to indentify hard to infer portions of the text. 
