# LeakCanaryNote
内存泄露以及内存溢出

内存溢出（OOM）：程序向系统申请的内存空间超出了系统能给的。
内存泄露：程序在向系统申请分配内存空间后，再使用完毕后未释放，使得一直占用内存单元，程序却无法使用该内存单元，内存泄露累计的结果是内存溢出。

Java是在JVM所虚拟的内存环境中运行的。
JVM内存分为三个区：
  1：栈（stack）--后进先出，只存储基本类型和对象的引用。
  2：堆（heap）--存放由new创建的对象和数组，并且被所有线程共享。
  3：方法区（method）--静态区，包含所有的class和static变量，并且被所有的线程共享。

垃圾回收（GC）机制：垃圾回收可以清空堆中不再使用的对象，java中通过对象的引用来使用对象，如果没有引用指向对象，对象为不可达，垃圾回收将回收此类对象。
内存泄露的原因：持有对象的强引用导致对象无法被GC回收。

引用类型：使程序能更加灵活的控制对象的生命周期。
  1：强引用： A a = new A();
  2：软引用： A a = new A(); SoftReference<A> soft = new SoftReference<A>(a);
  3: 弱引用： A a = new A(); WeakReference<A> soft = new WeakReference<A>(a);
  4：虚引用： PhantomReference(T referent, ReferenceQueue<? super T> q)

Android中会造成内存泄漏的常见情景：
  1：全局进程的static变量。
  2：活在Activity生命周期之外的线程。

Android app的检测工具：https://github.com/square/leakcanary
