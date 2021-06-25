## 关于条件变量
适用于生产者和消费者问题
```
while (bsem_p->v != 1) {
    pthread_cond_wait(&bsem_p->cond, &bsem_p->mutex); // unlock
    // lock
}
```
pthread_cond_broadcast：广播，通知所有的wait线程
1.假设仓库为空，有2个消费者在等待商品，设为C1和C2

2.假设生产者只生产了1件商品，然后调用pthread_cond_broadcast，则C1和C2都会得到通知

3.假设C1比C2先得到通知，然后加锁把商品消费了，并且解锁，这时C2就能拿到锁，但是此时商品已经没有了，如果此时C2不做检测，则会出现数据同步问题


https://angledark0123.pixnet.net/blog/post/51919620
