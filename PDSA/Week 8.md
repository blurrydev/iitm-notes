# Divide and Conquer - Counting  Inversions

#### Recommender System

Suppose there are movies `A B C D E`
So me and my friends are to rate this movies from 1 to 5

Let's say my ratings are `D A C B E`
My friend's ratings are `A E D C B`

Now we compare pairs and see the preference. Example: `A C`, both me and my friend prefer movie `A` more than movie `C`.

But when it comes to `B E`, I like movie `B` more than movie `E` but my friend likes the exact *opposite*. This is called an **Inversion**.

##### Inversions
In a list of `n` 
Inversions can range from:

- `0` : There are no inversions so the rankings are *identical*.
- `n(n-1)/2` : Every pair is inverted so the rankings are *complete opposite*.
