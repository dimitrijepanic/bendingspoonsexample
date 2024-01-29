# Amount of time to infect a binary tree
``` java
@Getter
// this class is needed because of the edge case when we reach NULL pointer
 class Result{
        int height;
        boolean found;
        Result(int height, boolean found){
            this.height = height;
            this.found = found;
        }
    }
```

``` java
// we are searching for the longest path from the starting node
int maxPath = 0;
    public Result amountOfTime(TreeNode root, int start){
        if(root == null) return new Result(0, false);

        Result left = traverseTree(root.left, start);
        Result right = traverseTree(root.right, start);

        // the initial point of infection - when we find it we are searching for the longest path from that point
        // here we reset the value of the length of path
        if(root.val == start) {
            // maxPath needs to be compared with the height of left and right subtree
            maxPath = Math.max(Math.max(left.h, right.h), maxPath);
            return new Result(0, true);
        }

       // if the start hasn't been found we have to decide are we going to return
       // the left or the right path length
       // we return the longer one
        if(!left.found && !right.found){
            // maxPath needs to be compared with the height of left and right subtree increased by 1 (current node)
            maxPath = Math.max(Math.max(left.h, right.h) + 1, maxPath);
            return new Result(Math.max(left.h, right.h) + 1, false);
        }

       // if the start has been found it means it is in found of the subtrees
       // meaning we have to check the path that goes through the current node 
        maxPath = Math.max(maxPath, left.h + right.h + 1);
       // we return the longer of the left or right subtree heights because we are searching for the longest path
      // that goes through the current node (it can either go to the left or right child, not both)
        return new Result(left.found ? left.h + 1 : right.h + 1, true);
    }
```
