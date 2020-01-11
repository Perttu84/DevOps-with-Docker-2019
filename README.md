# DevOps with Docker 2019
## 1.1
![1.1 solution](/images/1_1_solution.png)

## 1.2
I have some images I will still use, so I won't remove all images, but I hope that removing the nginx image I won't be using will be enough and prove that I know how to remove images.
![1.2 solution](/images/1_2_solution.png)

## 1.3
The password is `basics` and the secret message is `This is the secret message`.
```
docker run -it devopsdockeruh/pull_exercise
Give me the password: basics
You found the correct password. Secret message is:
"This is the secret message"
```

## 1.4
The secret message is "Docker is easy"
Commands given where
```
docker run -d devopsdockeruh/exec_bash_exercise
553c2d3ce22b091dacb866706794a351452493307cad9c2e350f2c47138aa54f
docker exec -it 55 bash
tail -f ./logs.txt
```