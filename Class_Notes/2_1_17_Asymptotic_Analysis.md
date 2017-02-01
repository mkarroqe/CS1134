## Asymptotic Analysis
#### Example
Show that 3n^2 + 6n - 15 = bigtheta(n^2)
##### Proof:
Take c1 = _______
     c2 = _______
     n0 = _______
    
Where do we start? by sketching some shit ok here we go

3n^2 = 3n^2 + 0 <= **3n^2 + 6n - 15** <= 3n^2 + 6n <= 3n^2 + 6n^2 = 9n^2 (we make it bigger by subtracting 15, but it's still not ??)

ok so now we can make c1 = 9 and c2 = 3 for some reason, i will consult the textbook and report back
n0 = 3

ok so here's the proof:
for all n >= 3 we have:
I) **3n^2 + 6n - 15** <= 3n^2 + 6n <= 3n^2 + 6n^2 = 9n^2
II) Since n >= 3 ==> 6n >= 18 >= 15 ==> 6n >= 15 ==> 6n-15 >= 0
    Therefore for n >= 3 we have:
    3n^2 + 6n - 15 >= 3n^2 + 0 = 3n^2
                   ^6n-15 >=0
III) All together we get that for n >= 3:
     3n^2 <= 3n^2 + 6n - 15 <= 9n^2
                   
"I'm supposed to look for two multiplicand of g that bind f from below and above"
===
