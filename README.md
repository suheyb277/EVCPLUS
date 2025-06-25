# EVCPLUS
import java.util.Scanner;

public class EVCPLUS {

    static Scanner input = new Scanner(System.in);
    static double balance = Math.random() * 100;
    static final int PASSWORD = 2426;

    // adeegyada la heli karo ee EvcPlus waa 1_9
    static String[] mainMenuOptions = {
            "1. Fiiri Haraaga",
            "2. Adeegyada Kaarka",
            "3. Bixinta Biilka",
            "4. Wareejin EVCPlus",
            "5. Warbixin Degdeg ah",
            "6. Salaam Bank",
            "7. Xakameyn & Dejinta",
            "8. Taaj Service",
            "9. Bill Payment"
    };

    public static void main(String[] args) {
        System.out.println("EVCPLUS - Nidaamka Lacagta");

        System.out.print("1: Geli furaha sirta ah ee adeegga: ");
        String code = input.next();

        if (checkCode(code)) {
            System.out.print("2: Geli lambarka sirta: ");
            int pin = input.nextInt();
            if (checkLogin(pin)) {
                int option = mainMenu();
                selectOption(option);
            }
        } else {
            System.out.println("Furaha lama garanayo. Adeegso *770# si aad u gasho.");
        }
    }

    public static boolean checkCode(String code) {
        return code.equals("*770#");
    }

    public static boolean checkLogin(int enteredPin) {
        int attempts = 3;
        while (attempts >= 0) {
            if (enteredPin == PASSWORD) {
                return true;
            } else {
                if (attempts == 0) break;
                System.out.println("Lambarka sirta waa khalad. Isku day mar kale.");
                System.out.print("Geli lambarka sirta (Fursado: " + attempts + "): ");
                enteredPin = input.nextInt();
            }
            attempts--;
        }
        System.out.println("Fursadaha oo dhan waa la isticmaalay. Fadlan isku day mar kale goor dambe.");
        return false;
    }

    public static int mainMenu() {
        System.out.println("\n>> EVCPLUS Adeegyada La Heli Karo <<");
        for (String option : mainMenuOptions) {
            System.out.println(option);
        }
        System.out.print("Fadlan dooro lambarka adeegga (1 ilaa 9): ");
        return input.nextInt();
    }

    // Dooro adeegyada loo bahanyahay ee EVCPLUS
    public static void selectOption(int option) {
        switch (option) {
            case 1: showBalance();
                break;
            case 2: kaarkaHadalka();
                break;
            case 3: bixintaBiil();
                break;
            case 4: wareejiEVCPlus();
                break;
            case 5: warbixinKooban();
                break;
            case 6: salaamBank();
                break;
            case 7: maareynta();
                break;
            case 8: taajService();
                break;
            case 9: billPayment();
                break;
            default:
                System.out.println("Doorasho khaldan. Fadlan dooro tiro sax ah.");
        }
    }

    public static void showBalance() {
        System.out.printf("[-EVCPlus-] Haraagaagu waa $%.2f%n", balance);
    }

    public static void kaarkaHadalka() {
        System.out.println("Kaarka hadalka:");
        System.out.println("1. Ku Shubo Airtime");
        System.out.println("2. Ugu Shub Airtime");
        System.out.println("3. MIFI Packages");
        System.out.println("4. Ku shubo Internet");
        System.out.println("5. Ugu shub qof kale (MMT)");
        System.out.print("Dooro mid: ");
        int dooro = input.nextInt();
        switch (dooro) {
            case 1:
                System.out.print("lacagta la doonayo: ");
                double airtime = input.nextDouble();
                if (airtime <= balance) {
                    System.out.print("Xaqiiji (1 = Haa, 0 = Maya): ");
                    String c1 = input.next();
                    if (c1.equals("1")) {
                        balance -= airtime;
                        System.out.printf("Ku shubid guuleysatay: $%.2f | Haraaga: $%.2f%n", airtime, balance);
                    }
                }
                break;
            case 2:
                System.out.print("Lambarka qofka: ");
                String num = input.next();
                System.out.print("lacagta: ");
                double amt = input.nextDouble();
                if (amt <= balance) {
                    System.out.print("Xaqiiji (1 = Haa, 0 = Maya): ");
                    String c2 = input.next();
                    if (c2.equals("1")) {
                        balance -= amt;
                        System.out.printf("U shubid guuleysatay: $%.2f --> %s | Haraaga: $%.2f%n", amt, num, balance);
                    }
                }
                break;
            case 3:
                System.out.println("MIFI adeegyada wali lama furin.");
                break;
            case 4:
                System.out.print("lacagta internet: ");
                double netAmt = input.nextDouble();
                if (netAmt <= balance) {
                    System.out.print("Xaqiiji (1 = Haa, 0 = Maya): ");
                    String c3 = input.next();
                    if (c3.equals("1")) {
                        balance -= netAmt;
                        System.out.printf("Internet la shubay: $%.2f | Haraaga: $%.2f%n", netAmt, balance);
                    }
                }
                break;
            case 5:
                System.out.print("Lambarka: ");
                String mmt = input.next();
                System.out.print("lacagta: ");
                double mmtAmt = input.nextDouble();
                if (mmtAmt <= balance) {
                    System.out.print("Xaqiiji (Haa/Maya): ");
                    String c4 = input.next();
                    if (c4.equalsIgnoreCase("Haa")) {
                        balance -= mmtAmt;
                        System.out.printf("U shubid (MMT): $%.2f --> %s | Haraaga: $%.2f%n", mmtAmt, mmt, balance);
                    }
                }
                break;
            default:
                System.out.println("Doorasho aan jirin.");
        }
    }

    public static void bixintaBiil() {
        System.out.println("Bixi Biil:");
        System.out.println("1. Post Paid");
        System.out.println("2. Ku Libso");
        System.out.print("Dooro: ");
        int bOpt = input.nextInt();
        System.out.print("Qadarka: ");
        double amount = input.nextDouble();
        if (amount <= balance) {
            balance -= amount;
            System.out.printf("Lacagta waa la bixiyey: $%.2f | Haraaga: $%.2f%n", amount, balance);
        } else {
            System.out.println("Haraaga kuguma filna.");
        }
    }

    public static void wareejiEVCPlus() {
        System.out.print("Lambarka: ");
        String rec = input.next();
        System.out.print("lacagta: ");
        double amt = input.nextDouble();
        if (amt > 0 && amt <= balance) {
            System.out.print("Xaqiiji wareejinta (1 = Haa): ");
            String conf = input.next();
            if (conf.equals("1")) {
                balance -= amt;
                System.out.printf("Wareejin guuleysatay: $%.2f --> %s | Haraaga: $%.2f%n", amt, rec, balance);
            }
        }
    }

    public static void warbixinKooban() {
        System.out.println("Warbixin Kooban:");
        System.out.println("1. Waxqabadkii ugu danbeeyay");
        System.out.println("2. Wareejintii ugu danbeysay");
        System.out.println("3. Iibsashadii ugu danbeysay");
        System.out.println("4. 3-dii fal ee ugu danbeysay");
        System.out.println("5. Email ii soo dir");
        System.out.print("Dooro: ");
        int opt = input.nextInt();
        switch (opt) {
            case 1: case 2: case 3: case 4:
                System.out.println("Falkan waa la helay (tusaale).");
                break;
            case 5:
                System.out.print("Email-ka ma rabi inaad hesho? (Haa/Maya): ");
                String yesNo = input.next();
                if (yesNo.equalsIgnoreCase("Haa")) {
                    System.out.println("Email ayaa laguugu soo diri doonaa.");
                }
                break;
            default:
                System.out.println("Doorasho aan sax ahayn.");
        }
    }

    public static void salaamBank() {
        System.out.println("Salaam Bank:");
        System.out.println("1. itus Haraaga");
        System.out.println("2. Lacag dhigasho");
        System.out.println("3. Lacag qaadasho");
        System.out.println("4. Ka wareeji EVCPlus");
        System.out.print("Dooro: ");
        int opt = input.nextInt();
        System.out.print("lacagta: ");
        double amount = input.nextDouble();
        if (opt == 1) {
            System.out.printf("Haraaga Salaam Bank: $%.2f%n", balance);
        } else if (amount <= balance && amount > 0) {
            balance += (opt == 2) ? amount : -amount;
            System.out.printf("Hawlgalku wuu dhammaaday. Haraaga: $%.2f%n", balance);
        } else {
            System.out.println("lacagta lama oggola ama haraaga kuma filna.");
        }
    }

    public static void maareynta() {
        System.out.println("Maareynta Adeegga:");
        System.out.println("1. Bedel PIN");
        System.out.println("2. Bedel Luqadda");
        System.out.println("3. Wargelin Mobile Lumay");
        System.out.println("4. Xiro lacagta");
        System.out.println("5. Celinta lacag qaldantay");
        System.out.println("6. Ka bax");
        System.out.print("Dooro: ");
        int opt = input.nextInt();
        if (opt >= 1 && opt <= 6) {
            System.out.println("Doorashada waa la fuliyey (tusaale).");
        } else {
            System.out.println("Fadlan dooro tiro sax ah.");
        }
    }

    public static void billPayment() {
        System.out.println("Bill Payment:");
        System.out.println("1. Itus Haraaga Bill-ka");
        System.out.println("2. Bixi Bill oo dhan");
        System.out.println("3. Bixi qayb ka mid ah");
        System.out.print("Dooro: ");
        int opt = input.nextInt();
        if (opt == 1) {
            System.out.println("Haraaga Bill-ka waa: $50.00");
        } else if (opt == 2 || opt == 3) {
            System.out.print("Geli lacagta: ");
            double amt = input.nextDouble();
            if (amt <= balance) {
                balance -= amt;
                System.out.printf("Bill-ka waa la bixiyay: $%.2f | Haraaga: $%.2f%n", amt, balance);
            } else {
                System.out.println("Haraaga kuma filna.");
            }
        } else {
            System.out.println("Doorasho khaldan.");
        }
    }

    public static void taajService() {
        System.out.println("Taaj Services:");
        System.out.println("1. Dir Lacag");
        System.out.println("2. Qaado Lacag");
        System.out.println("3. Kaarka Taaj");
        System.out.print("Dooro: ");
        int opt = input.nextInt();
        switch (opt) {
            case 1:
                System.out.println("Dir Lacag (tusaale ahaan).");
                break;
            case 2:
                System.out.println("Qaado Lacag (tusaale ahaan).");
                break;
            case 3:
                System.out.println("Macluumaadka Kaarka Taaj (tusaale ahaan).");
                break;
            default:
                System.out.println("Doorasho aan sax ahayn.");
        }
    }
}
