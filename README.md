### 1. **Prototype** — Copy Constructors

**Description**: The **Prototype** pattern allows for creating a new object by copying an existing one. In this code, this is implemented through copy constructors that take an object of the same type and initialize a new object with the same field values.

**Locations**:
   - **Class `ElettronicDevice`**:
     ```java
     public ElettronicDevice(ElettronicDevice i) {
         this.name = i.getName();
         this.id = i.getId();
         this.producer = i.getProducer();
         this.price = i.getPrice();
         this.amount = i.getAmount();
     }
     ```
     This constructor creates a copy of the `ElettronicDevice` object by copying its data. This allows passing objects by value rather than by reference.

   - **Class `Admin`**:
     ```java
     public Admin(Admin a) {
         super(a.getName(), a.getSurname(), a.getUsername(), a.getPassword());
     }
     ```
     The copy constructor for `Admin` uses the fields of an existing `Admin` object to initialize a new one.

   - **Class `Client`**:
     ```java
     public Client(final Client registerClient) {
         super(registerClient.getName(), registerClient.getSurname(), registerClient.getUsername(), registerClient.getPassword());
         this.address = registerClient.getAddress();
     }
     ```
     A copy constructor for `Client` that creates a copy of a client with the same information.

   - **Class `Employee`**:
     ```java
     public Employee(Employee emp) {
         super(emp.getName(), emp.getSurname(), emp.getUsername(), emp.getPassword());
     }
     ```
     This constructor creates a copy of the `Employee` object.

### 2. **Iterator** — Iterating over Collection Elements

**Description**: The **Iterator** pattern allows sequential access to the elements of a collection without exposing its underlying representation. In this code, the built-in Java iterators are used to traverse lists.

**Locations**:
   - **Method `addEmployee` in `Admin` class**:
     ```java
     public boolean addEmployee(final List<Employee> list, String name, String surname, String username, String password) {
         for (Employee i : list) {
             if (i.getUsername().equals(username)) return true;
         }
         list.add(new Employee(name, surname, username, password));
         return false;
     }
     ```
     Here, the `Iterator` pattern is used to check for the existence of an `Employee` with the same `username`.

   - **Method `rmvEmployee` in `Admin` class**:
     ```java
     public boolean rmvEmployee(final List<Employee> list, String username) {
         for (Employee e : list) {
             if (e.getUsername().equals(username)) {
                 list.remove(e);
                 return false;
             }
         }
         return true;
     }
     ```
     This method iterates through the list of employees and removes the employee with the matching `username` using an `Iterator`.

   - **Method `addProduct` in `Admin` class**:
     ```java
     public int addProduct(final List<ElettronicDevice> list, String name, int id, String producer, float price, int amount) {
         for (ElettronicDevice i : list) {
             if (i.getId() == id) return 3;
         }
         list.add(new ElettronicDevice(name, id, producer, price, amount));
         return 0;
     }
     ```
     The method iterates through devices in the list to check if a device with the same `id` already exists.

   - **Method `searchProduct` in `Client` class**:
     ```java
     for (ElettronicDevice e : list) {
         if (name.equalsIgnoreCase(e.getName()) || (name.equals(""))) {
             elprint.add(e);
             if ((!producer.equalsIgnoreCase(e.getProducer())) && (!(producer.equals("")))) {
                 elprint.remove(e);
             }
         }
     }
     ```
     This method uses an `Iterator` to filter the list of devices based on search criteria.

   - **Method `orderProduct` in `Client` class**:
     ```java
     for (ElettronicDevice i : elDev) {
         if (i.getId() == id) {
             int qnt = Integer.parseInt(amount);
             if ((qnt > 0) && (qnt <= i.getAmount())) {
                 // Logic for ordering the product
                 return 0;
             } else return 1;
         }
     }
     return 2;
     ```
     This method iterates through the available products (`elDev`) to find the product by `id` and check if there is enough quantity to fulfill the order.

   - **Method `addAmount` in `Employee` class**:
     ```java
     for (ElettronicDevice i : elDev) {
         if (i.getId() == id) {
             int q;
             try {
                 q = Integer.parseInt(amount);
                 if (q > 0) {
                     i.setAmount(i.getAmount() + q);
                     return 0;
                 } else return 1;
             } catch (NumberFormatException e) {
                 return 2;
             }
         }
     }
     for (ElettronicDevice j : buyElDev) {
         if (j.getId() == id) {
             int q;
             try {
                 q = Integer.parseInt(amount);
                 if (q > 0) {
                     j.setAmount(j.getAmount() + q);
                     elDev.add(buyElDev.remove(buyElDev.indexOf(j)));
                     return 0;
                 } else return 1;
             } catch (NumberFormatException e) {
                 return 2;
             }
         }
     }
     return 3;
     ```
     In this method, the `Iterator` is used to iterate over two lists of devices (`elDev` and `buyElDev`) and update the quantity of a product based on its `id`.

In summary, the **Prototype** pattern is utilized in the copy constructors, while the **Iterator** pattern is used for processing lists of employees and devices throughout the code.
