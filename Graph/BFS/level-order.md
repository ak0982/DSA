class Solution
{
    public:
    //Function to return the level order traversal of a tree.
    vector<int> levelOrder(Node* node)
    {
      //Your code here
        vector<int>res;
        queue<Node*>q;
        if(!node)
        return res;
        
        q.push(node);
        while(q.size()>0)
        {
            Node * temp=q.front();
            res.push_back(temp->data);
            
            q.pop();
            if(temp->left)
            {
               q.push(temp->left); 
                
            }
            if(temp->right)
            {
               q.push(temp->right); 
                
            }
        }
        return res;
    }
};



/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        queue<TreeNode*> qe1;
        qe1.push(root);
        while(!qe1.empty()) {
            int n  = qe1.size();
            vector<int>temp;
            for(int  i = 0; i<n ;i++) {
                TreeNode* curr = qe1.front();
                qe1.pop();
                temp.push_back(curr->val);
                if(curr->left) qe1.push(curr->left);
                if(curr->right) qe1.push(curr->right);
            }
            
            ans.push_back(temp);
        }
        
        return ans;
        
    }
};
