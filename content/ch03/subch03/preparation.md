# Preparation

You can start with copying the content of `lab_4/myrouter.py` to `lab_5/myrouter.py`.

1. Create a directory named `lab_5` in `switchyard`.
2. Copy `lab_4/start_mininet.py` to `lab_5/start_mininet.py`.
3. Copy `lab_4/myrouter.py` to `lab_5/myrouter.py`.
4. Copy `lab_4/forwarding_table.txt` to `lab_5/forwarding_table.txt`.

Though we will provide the test files, they are incomprehensible. So you should still write test scenarios that test all aspects of your code. You can find our test files below. Download it and you will use it to test your switch later. You can unzip the test files we provide into the folder `lab_5`.

[Download compiled test cases here](https://box.nju.edu.cn/d/123a70ac8ff34595b18f/).

Finally, your project will look like

```
switchyard
  ├─docs/
  ├─.../
+ ├─lab_5/
+ │ ├─myrouter.py
+ │ ├─forwarding_table.txt
  │ ├─...
+ │ └─start_mininet.py
  ├─.gitignore
  └─...
```

> [!WARNING]
> All of your modifications should be done on the files under your directory `lab_5`. We will check and compare the **git commits** to judge the originality of your work. So remember to commit every time you complete one small task.
