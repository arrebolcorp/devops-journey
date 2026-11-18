# Pipes and Redirections

##  1. What is the difference between `>` and `>>`?
`>` overwrite the file of destiny (remove all the previous content), while the `>>` add a at the final of the file without remove the previous values.

## 2. What does command `>` out.txt `2>&1` do?
Redirecting mean while `stdout` the standard output stream that the standard error steam `stderr` from the file `out.txt`. The operator `>` sends the normal output to the file and 2>&1 redirecting the errors at the same time.

## 3. Why does sudo echo hi > /srv/x fail, while echo hi | sudo tee /srv/x works?
Because the function of tee helps how utility for copying standard input to standard output. So, in this case the pipe `|` helps to manage de order actions, the shell read and run the commands lines of left to right, if a command do interference, the command line stop and back the error o failed.

## What would happen if you ran Tuesday’s echo ... > hello.sh twice?
Be overwrite the first text because `>>` don't add new lines if else overwrite with `>`.

## In Step 5, why do we use sort before uniq -c?
`uniq` only can read and counting duplicated data if are consecutives. When use `sort` first group all the lines that was equals for that `uniq -c` can count correctly all it.
