<!-- doc.py -->

Бинарное дерево поиска
Левый наследник всегда меньше правого.
Для балансировки: CartesianTree? Декартово дерево поиска?
``` java
public class BinaryTree<T extends Comparable<T>> implements SearchTree<T> {
    /**
     * Корневой элемент дерева
     */
    public TreeNode root = null;

    /**
     * Добавление нового значения в дерево поиска
     *
     * @param value добавляемое значение
     */
    @Override
    public void add(T value) {
        TreeNode newNode = new TreeNode(value);

        if (root == null) {
            root = newNode;
            return;
        }
        TreeNode cur = root;
        // Бесконечный цикл, т.к. мы выходим только когда нашли узел
        // к которому можем "подвесить" новый узел, и тогда мы выходим
        // по return
        while (true) {
            if (value.compareTo(cur.value) > 0) {
                if (cur.right == null) {
                    // Мы нашли нужный узел, подвешиваем
                    cur.right = newNode;
                    return;
                }
                // Спускаемся "направо"
                cur = cur.right;
            } else {
                if (cur.left == null) {
                    // Мы нашли нужный узел
                    cur.left = newNode;
                    return;
                }
                // Спускаемся "налево"
                cur = cur.left;
            }
        }
    }

    /**
     * Поиск значения в дереве поиска
     *
     * @param value Значение
     * @return найдено ли значение?
     */
    @Override
    public boolean find(T value) {
        // Спускаемся вниз по дереву поиска
        TreeNode cur = root;
        while (cur != null) {
            // Нашли узел с нужным значением
            if (cur.value.equals(value))
                return true;
            // Выбираем куда идти дальше
            cur = (value.compareTo(cur.value) > 0) ? cur.right : cur.left;
        }
        return false;

    }

    @Override
    public int deep() {
        return (root == null) ? 0 : root.deep();
    }

    /**
     * Узел дерева
     */
    class TreeNode {
        public T value;
        public TreeNode left = null;
        public TreeNode right = null;

        public TreeNode(T value) {
            this.value = value;
        }

        /**
         * @return глубина дерева
         */
        public int deep() {
            int res = 1;
            if (left != null)
                res = max(res, left.deep() + 1);
            if (right != null)
                res = max(res, right.deep() + 1);
            return res;
        }
    }
}
```

[src/main/java/BinaryTree.java](src/main/java/BinaryTree.java)

``` java
        // Интерфейс =  Класс с реализацией этого интерфейса
        BinaryTreeNode<Integer> tree = new BinaryTreeNode<>();
        assertFalse(tree.find(3));
        tree.add(3);
        assertTrue(tree.find(3));
        assertFalse(tree.find(2));

        // Добавить новое значение
        tree.add(2);
        assertTrue(tree.find(2));
        assertTrue(tree.find(3));

        // Добавляем узел с большим значением
        tree.add(334);
        assertTrue(tree.find(2));
        assertTrue(tree.find(3));
        assertTrue(tree.find(334));
        assertFalse(tree.find(7789));
```

[src/test/java/BinaryTreeTest.java](src/test/java/BinaryTreeTest.java)

Set - множество элементов
-------------------------
Основные операции на множествах
add(value) добавить в множество
isEmpty() - пусто ли множество?
size() - количество элементов в списке
``` java
        assertTrue("Множество пусто", s.isEmpty());
        s.add(7);
        assertFalse("Теперь уже не пусто", s.isEmpty());
        s.add(7);
        assertEquals("В множестве 1 элемент т.к. значения совпадают", 1, s.size());
        s.add(10);
        assertEquals("В множестве 2 элемента", 2, s.size());
```

get(index) - получить элемент с заданным индексом
Добавляем сразу массив элементов
remove(Object o) - удаление элемента по значению
contains(Object o) - проверяет наличие элемента в множестве
Проверка, содержит ли одно множество другое множество
[src/test/java/SetTest.java](src/test/java/SetTest.java)

