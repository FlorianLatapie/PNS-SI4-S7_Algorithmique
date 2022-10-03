# TD2 
## Exo 1 
```dot
digraph exo1 {
    // lire | ecrire | deplacement (D) 
    q0 -> q1 [label="1|1|D"];
    q1 -> q1 [label="1|1|D"];
    q1 -> q2 [label="0|0|D"];
    q2 -> q3 [label="1|1|D"];
    q3 -> q3 [label="1|1|D"];
    q3 -> qf [label="B|B|S"];
    
    // etat poubelle 
    q0 -> poubelle [label="0|0|S\nB|B|S"];
    q1 -> poubelle [label="B|B|S"];
    q2 -> poubelle [label="0|0|S\nB|B|S"];
    q3 -> poubelle [label="0|0|S"]
}
```
// the same in mermaid
```mermaid
graph TB
    q0((q0)) --> | 1/1/D | q1((q1))
    q1((q1)) --> | 1/1/D | q1((q1))
    q1((q1)) --> | 0/0/D | q2((q2))
    q2((q2)) --> | 1/1/D | q3((q3))
    q3((q3)) --> | 1/1/D | q3((q3))
    q3((q3)) --> | B/B/S | qf((qf))

    %% etat poubelle
    q0((q0)) --> | 0/0/S<br/>B/B/S | poubelle((poubelle))
    q1((q1)) --> | B/B/S | poubelle((poubelle))
    q2((q2)) --> | 0/0/S<br/>B/B/S | poubelle((poubelle))
    q3((q3)) --> | 0/0/S | poubelle((poubelle))
```


![exo1](exo1.svg)

## Exo 2
```dot
digraph exo2_1{
    // lire,lire2 | ecrire,ecire2 | deplacement, deplacement2 
    q0 -> q0 [label="1,1|1,1|D,D\n0,0|0,0|D,D"];
    q0 -> q1 [label="b,b|b,b|D,D"];
    q1 -> q2 [label="0,0|0,0|G,G\n0,1|0,1|G,G\n1,0|1,0|G,G\n1,1|1,1|G,G"];
    q2 -> q1 [label="0,0|0,0|G,S\n0,1|0,1|G,S\n1,0|1,0|G,S\n1,1|1,1|G,S"];
    q2 -> q3 [label="b,b|b,b|D,D"];
    q3 -> q3 [label="1,1|1,1|D,D\n0,0|0,0|D,D"];
    q3 -> qf [label="0,b|0,b|D,D\n1,b|1,b|D,D"];

}
```
// the same in mermaid
```mermaid
graph TB
    q0((q0)) --> | 1/1/D<br/>0/0/D | q0((q0))
    q0((q0)) --> | b/b/D | q1((q1))
    q1((q1)) --> | 0/0/G<br/>0/1/G<br/>1/0/G<br/>1/1/G | q2((q2))
    q2((q2)) --> | 0/0/G/S<br/>0/1/G/S<br/>1/0/G/S<br/>1/1/G/S | q1((q1))
    q2((q2)) --> | b/b/D | q3((q3))
    q3((q3)) --> | 1/1/D<br/>0/0/D | q3((q3))
    q3((q3)) --> | 0/b/D<br/>1/b/D | qf((qf))
```


![exo2-1](exo2-1.svg)

```dot
digraph exo2_2{
    // lire,lire2 | ecrire,ecire2 | deplacement, deplacement2 
    q0 -> q1[label="0|x|D\n1|y|D"];
    q0 -> q4[label="x|x|D\ny|y|D"];

    q1 -> q1[label="0|0|D\n1|1|D"];
    q1 -> q2[label="b|b|G\nx|x|G\ny|y|G"];
    
    q2 -> q3[label="0|x|G\n1|y|G"];
    
    q3 -> q3[label="0|0|G\n1|1|G"];
    q3 -> q0[label="x|x|D\ny|y|D"];
    
    q4 -> q5[label="y|1|G"];
    q4 -> q9[label="x|0|G"];

    q5 -> q5[label="x|x|G\ny|y|G"];
    q5 -> q6[label="b|b|D\n1|1|D\n0|0|D"];

    q6 -> q7[label="y|1|D"];
    
    q7 -> q7[label="x|x|D\ny|y|D"];
    q7 -> q8[label="0|0|D\n1|1|D"];
    
    q8 -> qf; 
    q8 -> q8[label="0|0|D\n1|1|D"];
    q8 -> q4[label="x|x|S\ny|y|S"];
    
    q9 -> q9[label="x|x|G\ny|y|G"];
    q9 -> q10[label="b|b|D\n1|1|D\n0|0|D"];
    
    q10 -> q7[label="x|0|D"];
}
```
// the same in mermaid
```mermaid
graph TB
    q0((q0)) --> | 0/x/D<br/>1/y/D | q1((q1))
    q0((q0)) --> | x/x/D<br/>y/y/D | q4((q4))

    q1((q1)) --> | 0/0/D<br/>1/1/D | q1((q1))
    q1((q1)) --> | b/b/G<br/>x/x/G<br/>y/y/G | q2((q2))

    q2((q2)) --> | 0/x/G<br/>1/y/G | q3((q3))

    q3((q3)) --> | 0/0/G<br/>1/1/G | q3((q3))
    q3((q3)) --> | x/x/D<br/>y/y/D | q0((q0))

    q4((q4)) --> | y/1/G | q5((q5))
    q4((q4)) --> | x/0/G | q9((q9))

    q5((q5)) --> | x/x/G<br/>y/y/G | q5((q5))
    q5((q5)) --> | b/b/D<br/>1/1/D<br/>0/0/D | q6((q6))

    q6((q6)) --> | y/1/D | q7((q7))

    q7((q7)) --> | x/x/D<br/>y/y/D | q7((q7))
    q7((q7)) --> | 0/0/D<br/>1/1/D | q8((q8))

    q8((q8)) --> | 0/0/D<br/>1/1/D | q8((q8))
    q8((q8)) --> | x/x/S<br/>y/y/S | q4((q4))
    q8((q8)) --> | 0/0/D<br/>1/1/D | qf((qf))

    q9((q9)) --> | x/x/G<br/>y/y/G | q9((q9))
    q9((q9)) --> | b/b/D<br/>1/1/D<br/>0/0/D | q10((q10))

    q10((q10)) --> | x/0/D | q7((q7))
```

![exo2-2](./exo2-2.svg)

## Exo 3
```dot
digraph exo_3{
  q0 -> q0[label="a|a|D"];
  q0 -> q1[label="B|B|G"];
  
  q1 -> q1[label="X|X|G\n0|0|G\n1|1|G"];
  q1 -> q2[label="B|0|D"];
  q1 -> q3[label="a|X|G"];
  
  q2 -> q2[label="X|X|D\n0|0|D\n1|1|D"];
  q2 -> qf[label="B|B|S"];
  q2 -> q0[label="a|a|D"];
  

  q3 -> q3[label="X|X|G\n0|0|G\n1|1|G"];
  q3 -> q1[label="a|a|G"];
  q3 -> q2[label="B|1|G"];
}
```
// the same in mermaid
```mermaid
graph TB
    q0((q0)) --> | a/a/D | q0((q0))
    q0((q0)) --> | B/B/G | q1((q1))
    q1((q1)) --> | X/X/G<br/>0/0/G<br/>1/1/G | q1((q1))
    q1((q1)) --> | B/0/D | q2((q2))
    q1((q1)) --> | a/X/G | q3((q3))
    q2((q2)) --> | X/X/D<br/>0/0/D<br/>1/1/D | q2((q2))
    q2((q2)) --> | B/B/S | qf((qf))
    q2((q2)) --> | a/a/D | q0((q0))
    q3((q3)) --> | X/X/G<br/>0/0/G<br/>1/1/G | q3((q3))
    q3((q3)) --> | a/a/G | q1((q1))
    q3((q3)) --> | B/1/G | q2((q2))
```

![exo3](exo3.svg)

## Exo 4
```dot
digraph exo_4{
  q0 -> q0[label="0,B|0,0|DD"];
  q0 -> q1[label="1,B|1,B|S,G"];
  
  q1 -> q1[label="1,0|1,0|D,G"];
  q1 -> qf[label="B,B|B,B|S,S"]
}
```
// the same in mermaid 
```mermaid
graph TB
    q0((q0)) --> | 0,B/0,0/DD | q0((q0))
    q0((q0)) --> | 1,B/1,B/S,G | q1((q1))
    q1((q1)) --> | 1,0/1,0/D,G | q1((q1))
    q1((q1)) --> | B,B/B,B/S,S | qf((qf))
```



![exo4](exo4.svg)

## Exo 5
```dot
digraph exo_5{
  q0 -> q1[label="a,B|A,X|D,D"];
  
  q1 -> q1[label="a,x|a,X|S,D"];
  q1 -> qf1[label="B,B|B,B|S,S"];
  q1 -> q2[label="a,B|a,X|S,D"];
  
  q2 -> q3[label="a,B|a,X|D,G"];
  
  q3 -> q3[label="a,X|a,X|D,G"];
  q3 -> q1[label="a,B|a,B|S,D"];
  q3 -> qf1[label="B,B|B,B|S,S"]
}
```
// the same in mermaid 
```mermaid
graph TB
    q0((q0)) --> | a,B/A,X/D,D | q1((q1))
    q1((q1)) --> | a,x/a,X/S,D | q1((q1))
    q1((q1)) --> | B,B/B,B/S,S | qf1((qf1))
    q1((q1)) --> | a,B/a,X/S,D | q2((q2))
    q2((q2)) --> | a,B/a,X/D,G | q3((q3))
    q3((q3)) --> | a,X/a,X/D,G | q3((q3))
    q3((q3)) --> | a,B/a,B/S,D | q1((q1))
    q3((q3)) --> | B,B/B,B/S,S | qf1((qf1))
```
![exo5](exo5.svg)

## Exo 6
```mermaid 
graph TB
    q0((q0)) --> | 0,B,B/B,0,B/D,D,S<br/>1,B,B/B,1,B/D,D,S | q0((q0))
    q0((q0)) --> | +,B,B/B,B,B/D,S,S | q1((q1))

    q1((q1)) --> | 0,B,B/B,B,0/D,S,D<br/>1,B,B/B,B,1/D,S,D | q1((q1))
    q1((q1)) --> | B,B,B/B,B,B/S,G,G | q2((q2))
    
    q2((q2)) --> | B,0,0/0,0,0/G,G,G<br/>B,1,0/1,1,0/G,G,G<br/>B,0,1/1,0,1/G,G,G<br/>B,B,0/0,B,0/G,G,G<br/>B,0,B/0,0,B/G,G,G<br/>B,B,1/1,B,1/G,G,G<br/>B,B,1/1,B,1/G,G,G<br/>B,1,B/1,1,B/G,G,G | q2((q2))
    q2((q2)) --> | B,1,1/0,1,1/G,G,G | q3((q3))
    q2((q2)) --> | B,B,B/B,B,B/S,S,S | qf((qf))

    q3((q3)) --> | B,0,1/0,0,1/G,G,G<br/>B,1,0/0,1,0/G,G,G<br/>B,1,1/1,1,1/G,G,G<br/>B,B,1/0,B,1/G,G,G<br/>B,1,B/0,1,B/G,G,G | q3((q3))
    q3((q3)) --> | B,0,0/1,0,0/G,G,G<br/>B,B,0/1,B,0/G,G,G<br/>B,0,B/1,0,B/G,G,G<br/>B,B,B/1,B,B/G,G,G | q2((q2))
```