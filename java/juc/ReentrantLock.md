### tryLock与lock区别

tryLock不阻塞，获取不到锁就放弃

lock阻塞，获取不到锁会一直等待

### ReentrantLock和synchronized区别

1.sychronized遇到异常，如果不 catch，锁会自动释放，ReentrantLock需要手动释放

2.synchronized是非公平锁，ReentrantLock是公平锁

3.sychronized没有tryLock机制

