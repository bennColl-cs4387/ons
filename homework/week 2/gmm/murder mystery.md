# Github Murder Mystery - Ons
## Initial cloning and recon
```
 git clone https://github.com/nivbend/gitstery.git
 cd gitstery/
 ls -la
 less instructions.txt
 git checkout gtpd-archive
 git status
 ls
 less residents.txt
 less instructions.txt
 git checkout HEAD^1
 ls
 git checkout gtpd-archive
 git status
 git checkout HEAD

 ```
 
 - According to the instructions, we need to find the access log pertaining to accessing **"BACKDOOR_332"**, so I will switch to that branch and look through the git log to figure out which incident matches our timeline

``` git log
 git checkout detectives/kpumbinner
 ls
 cd evidence
 ls
 cat access.log
 ls
 ls -la
 less access.log
 ls
 cd ../
 ls
 git log
 git checkout bd57df061ea29e7e88d6438b4140f3af4ae01eb5
 ls
 git log
 ls
 less evidence/access.log | grep BACKDOOR
 git checkout 23dbcfa6c0276e29f31c5dddfc9edf44bcf94cf2
 less evidence/access.log | grep BACKDOOR
 git checkout 40fa72a502ceac70f02fffad356e0b49f400dd86
 less evidence/access.log | grep BACKDOOR
 git checkout e21ce2e8b23cd40571eacbfbbcb772fb95529938
 less evidence/access.log | grep BACKDOOR
 git checkout 17d1e75b44cd4c61edc90e634f7a81383d4d57e2
 less evidence/access.log | grep BACKDOOR
 git log
 git checkout 5b96ff2008e52f940136d9f6a6e0323dbb6c6fe7
 less evidence/access.log | grep BACKDOOR
 ls
 git log
 git status
 git show bd57df061ea29e7e88d6438b4140f3af4ae01eb5
 git show 23dbcfa6c0276e29f31c5dddfc9edf44bcf94cf2
 git show 40fa72a502ceac70f02fffad356e0b49f400dd86
 c9983ccf05cbe4d8c3f6a8ff856e5e0c5f6a7565
 git show c9983ccf05cbe4d8c3f6a8ff856e5e0c5f6a7565
 git show 17d1e75b44cd4c61edc90e634f7a81383d4d57e2
 ks
 ls
 less residents.txt
 ```
 

 - Looks like we have three suspects to interrogate: 
```
d9289fe4 (Lyndon Huskupper   2019-07-14 12:06:00 +0000 19) BACKDOOR_332
09d0547f (Cosmo Siwkonk      2019-07-14 14:16:00 +0000 36) BACKDOOR_332
13611d85 (Brock Stuickard    2019-07-14 15:23:00 +0000 44) BACKDOOR_332
```
The first one does not match our timeline so we can discard it, now I will look through residents.txt to get their addresses and investigate those branches further

```
git tag
 git checkout street/wantage_close
 ls
 cd investigate
 less investigate
 git checkout 0c13ae7c245edbb787eb34a9809f0ae22ebf1c34
 ls -la
 cat investigate
 clear
 git checkout detectives/kpumbinner
 ls
 cd evidence
 ls
 git blame access.log
 git blame access.log | grep BACKDOOR
 cd ../
 cat residents.txt | Brock
 cat residents.txt | grep Brock
 git checkout beaconside
 git checkout streets/beaconside
 git checkout street/beaconside
 ls
 cat investigate
 git cat-file -p bef9c2d783e513bc78338d32e88747e6786fa3fc
 ls
 git checkout street/beaconside/9
 git status
 git log
 git log | grep Hyundai
 git log | grep party
 ls
 cd ../
 ls
 cd gitstery
 ls
 cd investigate
 l
 cat residents.txt | Cosmo
 cat residents.txt
 less residents.txt | grep Cosmo
 git checkout street/balcombe
 git checkout street/balcombe_close
 ls
 cat investigate
 git cat-file -p 94d83d846f410deb6a0b2450b01291471002ddca
 git log
 git log | grep 26 Balcome
 git log | grep 26 Balcom
 git log | grep 26
 git log
 git log | grep car
 git log
 git cat-file -p c8411c73e49372dbdb644beef2ea841b403fc476
 cd ~/
 ls -la
 less .bash_history
```

- According to Brock Stuickard, the suspect left off in a Green Hyundai, probably a rental.
- From other reports around the neighboorhood, Cosmo seems like they have a Green Hyundai, were not home, and not the best part of the community either
- It seems like we have our culprit, we can confirm our suspicion using the command given by the author `echo "Cosmo Siwkonk" | git hash-object --stdin | grep -iq -f /dev/stdin <(git show solution) && echo 'You found the murderer!' || echo 'No cigar, chief... Try again.'
- It returns `You found the murderer!`
## Useful Commands from this exercise
`git tag`
`git show`
`git log`
`git cat-file -p`
  
## Cleanup
I used this command to emit out the first space in the file which is the line number

`awk '{$1="";print $0}' FileName > NewFileName`