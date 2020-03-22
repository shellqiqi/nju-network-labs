# Preparation

There is an example of a router without anything implemented in `switchyard/examples/exercises/router/myrouter.py`. Let's start with it.

1. Create a directory named `lab_3` in `switchyard`.
2. Copy `examples/exercises/router/start_mininet.py` to `lab_3/start_mininet.py`.
3. Copy `examples/exercises/router/myrouter.py` to `lab_3/myrouter.py`.

Though we will provide the test files, they are incomprehensible. So you should still write test scenarios that test all aspects of your code. You can find our test files below. Download it and you will use it to test your router later. You can unzip the test files we provide into the folder `lab_3`.

[Download compiled test cases here](https://box.nju.edu.cn/d/123a70ac8ff34595b18f/).

Finally, your project will look like

```
switchyard
  ├─docs/
  ├─.../
+ ├─lab_3/
+ │ ├─myrouter.py
  │ ├─...
+ │ └─start_mininet.py
  ├─.gitignore
  └─...
```

> [!WARNING]
> All of your modifications should be done on the files under your directory `lab_3`. We will check and compare the **git commits** to judge the originality of your work. So remember to commit every time you complete one small task.
