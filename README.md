# Cocos2d-x 3.0 Performance Benchamrk

This document is a brief introduction of testing sample and performance standard. I take this benchmark from two aspects-language compare and resource utilization compare.

### Language Compare

This test is simply comparing the language performance by excuting `Loop`, `Callback` and `MAT4`. Take time consuming as the standard.

```cpp
// Loop

N = 1000;
i = 0;
while(i < N)
{
	i++;
}
```

```cpp
// Callback

N = 1000000;
i = 0;
sum = 0;
while(i < N)
{
	sum += add(i, 1);
}
```

```cpp
// mat4

N = 100000;
i = 0;
a = [...];
b = [...];
c = [...];
while(i < N)
{
	multiplayMatrix(a, b, c);
	i++;
}
```

####Device Overview

|             |`Android`   |`iOS`    |
|-------------|------------|---------|
|CPU          |600MHz      |1331MHz  |
|RAM          |256M        |1G       |
|OS           |Android 2.2 |iOS 7.03 |

####Testing Data

|`Android`    |Loop        |Callback        |MAT4        |
|-------------|------------|----------------|------------|
|JSB(JIT)     |3.7 ms      |8268 ms         |37899 ms    |
|Lua(JIT)     |0.8 ms      |304  ms         |899   ms    |
|C++          |0.1 ms      |31.5 ms         |295.4 ms    |

|`iOS`        |Loop        |Callback        |MAT4        |
|-------------|------------|----------------|------------|
|JSB          |1   ms      |609.1 ms        |9223  ms    |
|Lua          |0.3 ms      |109.9 ms        |581.7 ms    |
|C++          |0   ms      |0     ms        |29.6  ms    |


`More detials:`

[C++ project](https://github.com/gloryming/Language_Cpp)

[JSB project](https://github.com/gloryming/Language_JS)

[Lua project](https://github.com/gloryming/Language_Lua)

### Resource Utilization Comapre

This test is computing the memory consuming when adding 1000, 10000 and 100000 nodes in the scene.

```
N = 1000

i = 0

while(i < N)
{
	auto sprite = Sprite::create("HelloWorld.png");
	addChile(sprite);
	i++;
}
```

####Device Overview

|             |`iOS`    |
|-------------|---------|
|CPU          |1331MHz  |
|RAM          |1G       |
|OS           |iOS 7.03 |

####Testing Data

|`iOS`        |1000        |10000           |100000      |
|-------------|------------|----------------|------------|
|JSB          |2.1  M      |11.8   M        |128.6  M    |
|Lua          |0.7  M      |13.1   M        |118.6  M    |
|C++          |1.2  M      |11.2   M        |91.1   M    |
