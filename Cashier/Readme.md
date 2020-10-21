# Aplikasi Kasir
Aplikasi ini digunakan untuk menghitung total harga barang atau jasa yang diinputkan.

## Function
Dengan menginputkan nama barang/jasa dan menginputkan jumlah dan harganya maka aplikasi 
akan secara otomatis memperlihatkan subtotal dan total harga barang.

## Coding

### class item
```csharp
 class Item
    {
        private int id;
        public string title { get; set; }
        public int quantity { get; set; }
        public double price { get; set; }
        public double subtotal { get; set; }
        private string type;

        public Item(int id, string title, int quantity, double price, double subtotal, string type)
        {
            this.id = id;
            this.title = title;
            this.quantity = quantity;
            this.price = price;
            this.subtotal = subtotal;
            this.type = type;
        }
        public string getTitle()
        {
            return title;
        }

        public int getQuantity()
        {
            return quantity;
        }

        public string getType()
        {
            return type;
        }

        public double getPrice()
        {
            return price;
        }

        public double getSubTotal()
        {
            subtotal = price * quantity;
            return subtotal;
        }
    }
```
 pada class item ini dilakukan pendeklarasian variabel dan fungsi.

### class calculator
```csharp
class Calculator
    {
        private List<Item> listItem;
        private double total = 0;

        public Calculator()
        {
            this.listItem = new List<Item>();
        }

        public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }

        public double getTotal()
        {
            return total;
        }

        public List<Item> getListItem()
        {
            return listItem;
        } 
    }
```
Class ini digunakan untuk menghitung total harga

### main window
```csharp
public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator();
            listBox.ItemsSource = calculator.getListItem();
        }
```
mendeklarasikan nilai variabel dari class calculator

### AddButton_Click
```csharp
private void AddButton_Click(object sender, RoutedEventArgs e)
        {
            string title = itemNameBox.Text;
            int quantity = int.Parse(quantityBox.Text);
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);

            Item item = new Item(new Random().Next(), title, quantity, price, price, type);
            calculator.addItem(item);
            double total = calculator.getTotal();

            totalLabel.Content = string.Format("Rp. {0}", total);

            listBox.Items.Refresh();
        }
```
pada bagian aktif saat kita melakukan click pada button, code ini
digunakan untuk memasukkan data yang diinputkan ke dalam variabel dan menentukan tipe datanya. 
Dan sebagai letak dimana datanya dikembalikan.