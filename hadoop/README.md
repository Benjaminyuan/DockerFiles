
### usage

1. clone repository 
   
   ```
   $ git clone https://github.com/gtchaos/docker-for-hadoop.git
   ```

2. build hadoop cluster
   
   ```
   $ sh build.sh 
   ```

3. switch to hadoop user 

   When you attached master node, please run `su hadoop` in bash.
   
   ```
   root@hadoop-master:~# su hadoop
   ```

4. start hadoop
   
   ```
   hadoop@hadoop-master:~# ./start-hadoop.sh
   ```

5. run wordcount

   ```
   hadoop@hadoop-master:~# ./run-wordcount.sh 
   ```


