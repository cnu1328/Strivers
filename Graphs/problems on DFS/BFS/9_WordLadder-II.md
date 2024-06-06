# Word Ladder II

[Problem Link]()

## Approach - Use BFS

1. It is the variant of Word Ladder 1
2. we use Queue data structure to store the transformation sequences
3. loop until the queue is not empty
4. replace each charater of the word with 26 alphabets
5. If any replaced character word find in wordList, then append this word to sequence and push to queue.
6. use Set for searching and to verify the word is visited or not
7. Finally return the set of sequences


```Java

class Solution {
public:
    
    vector<vector<string>> findSequences(string beginWord, string endWord, vector<string>& wordList) {
        
        queue<vector<string>> que;
        vector<string> usedWord;
        unordered_set<string> st(wordList.begin(), wordList.end());
        
        que.push({beginWord});
        usedWord.push_back(beginWord);
        int level = 0;
        
        vector<vector<string>> ans;
        
        while(!que.empty()) {
            
            vector<string> sequence = que.front();
            que.pop();
            
            if(sequence.size() > level) {
                level++;
                
                for(string str : usedWord) {
                    st.erase(str);
                }
                
                usedWord.clear();
            }
            
         
            string word = sequence.back();
            
            if(word == endWord) {
                if(ans.size() == 0) {
                    ans.push_back(sequence);
                }
                
                else if(ans[0].size() == sequence.size()) {
                    ans.push_back(sequence);
                }
                
                else continue;
            }
            
            
            for(int j=0; j<word.length(); j++) {

                char original = word[j];

                for(char c = 'a'; c <= 'z'; c++) {
                    word[j] = c;

                    if(st.find(word) != st.end()) {
                        sequence.push_back(word);
                        usedWord.push_back(word);
                        que.push(sequence);
                        sequence.pop_back();

                    }
                }

                word[j] = original;
            }
            
        }
        
        
        return ans;
        
        
    }
};

```


## Complexity Analysis:

### Time Complexity: (TC depends on the input)

### Space Complexity: (SC depends on the input)