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
    public Result traverseTree(TreeNode root, int start){
        if(root == null) return new Result(0, false);

        Result left = traverseTree(root.left, start);
        Result right = traverseTree(root.right, start);

        // the path actually start from the starting node
        // here we reset the value of the length of path
        if(root.val == start) {
            maxPath = Math.max(Math.max(left.h, right.h), maxPath);
            return new Result(0, true);
        }

       // if the node hasnt been found we have to decide are we going to return
       // the left or the right path length
       // we return the longer one
        if(!left.found && !right.found){
            maxPath = Math.max(Math.max(left.h, right.h) + 1, maxPath);
            return new Result(Math.max(left.h, right.h) + 1, false);
        }

       // if the start has been found
       // return the longer
        maxPath = Math.max(maxPath, left.h + right.h + 1);
        return new Result(left.found ? left.h + 1 : right.h + 1, true);
    }
```
