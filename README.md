class Menu {
    String name;
    double price;
    String category;

    public Menu(String name, double price, String category) {
        this.name = name;
        this.price = price;
        this.category = category;
    }
}

public class Main {
    public static void main(String[] args) {
        Menu[] menuItems = {
            new Menu("Nasi Padang", 25000, "makanan"),
            new Menu("Ayam Goreng", 20000, "makanan"),
            new Menu("Es Teh", 5000, "minuman"),
            new Menu("Kopi", 8000, "minuman"),
            new Menu("Nasi Goreng", 30000, "makanan"),
            new Menu("Sate Ayam", 22000, "makanan"),
            new Menu("Jus Jeruk", 6000, "minuman"),
            new Menu("Air Mineral", 3000, "minuman")
        };

        double totalCost = 0;
        int totalItems = 0;
        int minumanGratis = 0;

        System.out.println("Selamat datang di Restoran XYZ!");

        System.out.println("Daftar Menu Makanan:");
        for (Menu menuItem : menuItems) {
            if (menuItem.category.equals("makanan")) {
                System.out.println(menuItem.name + " - Rp. " + menuItem.price);
            }
        }

        System.out.println("Daftar Menu Minuman:");
        for (Menu menuItem : menuItems) {
            if (menuItem.category.equals("minuman")) {
                System.out.println(menuItem.name + " - Rp. " + menuItem.price);
            }
        }

        // Memesan menu
        System.out.println("Pesan menu (maksimal 4 menu):");
        for (int i = 0; i < 4; i++) {
            System.out.print("Nama menu: ");
            String itemName = System.console().readLine();
            System.out.print("Jumlah: ");
            int quantity = Integer.parseInt(System.console().readLine());

            for (Menu menuItem : menuItems) {
                if (menuItem.name.equalsIgnoreCase(itemName)) {
                    totalCost += menuItem.price * quantity;
                    totalItems += quantity;

                    if (menuItem.category.equals("minuman")) {
                        minumanGratis += quantity / 2;
                    }
                }
            }

            System.out.print("Tambah menu lagi? (y/n): ");
            String continueOrder = System.console().readLine();
            if (!continueOrder.equalsIgnoreCase("y")) {
                break;
            }
        }

        // Menghitung total biaya
        double tax = totalCost * 0.1;
        double serviceCharge = 20000;

        if (totalCost > 100000) {
            totalCost -= totalCost * 0.1;
        }

        if (totalCost > 50000) {
            totalCost -= minumanGratis * menuItems[2].price; // Index 2 is "Es Teh"
        }

        // Mencetak struk pesanan
        System.out.println("\nStruk Pesanan:");
        System.out.println("Item - Jumlah - Harga");
        for (Menu menuItem : menuItems) {
            int quantity = 0;
            for (int i = 0; i < 4; i++) {
                if (menuItem.name.equalsIgnoreCase(menuItems[i].name)) {
                    quantity += totalItems;
                }
            }
            if (quantity > 0) {
                System.out.println(menuItem.name + " - " + quantity + " - Rp. " + menuItem.price * quantity);
            }
        }

        System.out.println("\nTotal Biaya: Rp. " + totalCost);
        System.out.println("Pajak (10%): Rp. " + tax);
        System.out.println("Biaya Pelayanan: Rp. " + serviceCharge);
    }
}
