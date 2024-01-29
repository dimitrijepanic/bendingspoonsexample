# Amount of time to infect a binary tree
``` java
@Getter
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
int maxPath = 0;
    public Result traverseTree(TreeNode root, int start){
        if(root == null) return new Result(0, false);

        Result left = traverseTree(root.left, start);
        Result right = traverseTree(root.right, start);

        if(root.val == start) {
            maxPath = Math.max(Math.max(left.h, right.h), maxPath);
            return new Result(0, true);
        }

        if(!left.found && !right.found){
            maxPath = Math.max(Math.max(left.h, right.h) + 1, maxPath);
            return new Result(Math.max(left.h, right.h) + 1, false);
        }

        maxPath = Math.max(maxPath, left.h + right.h + 1);
        return new Result(left.found ? left.h + 1 : right.h + 1, true);
    }
```
