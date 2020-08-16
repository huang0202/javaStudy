### LinedList集合

###  构造器
    1、无参构造器
     public LinkedList() {
        }
     创建一个空的链表
    
    2、将集合作为参数
    public LinkedList(Collection<? extends E> c) {
            this();
            addAll(c);
        }
    调用无参构造器生成一个空链表，在调用addAll(c) 
    
        **************************addAll(c) 调用重载的addAll方法
        public boolean addAll(int index, Collection<? extends E> c) {
            checkPositionIndex(index);
    
            Object[] a = c.toArray();
            int numNew = a.length;
            if (numNew == 0)
                return false;
    
            Node<E> pred, succ;
            if (index == size) {
                succ = null;
                pred = last;
            } else {
                succ = node(index);
                pred = succ.prev;
            }
    
            for (Object o : a) {
                @SuppressWarnings("unchecked") E e = (E) o;
                Node<E> newNode = new Node<>(pred, e, null);
                if (pred == null)
                    first = newNode;
                else
                    pred.next = newNode;
                pred = newNode;
            }
    
            if (succ == null) {
                last = pred;
            } else {
                pred.next = succ;
                succ.prev = pred;
            }
    
            size += numNew;
            modCount++;
            return true;
        }
 
 
 
 
 
 
 
### 成员变量
    1、 transient int size = 0;
    size 长度
    2、  transient Node<E> first;
    first指向第一个节点指针
    3、  transient Node<E> last;
    last:指向最后一个节点指针




