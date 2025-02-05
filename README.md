[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/i0lX2DJF)


class Video {
    private String title;
    private boolean checkedOut;
    private double totalRating;
    private int ratingCount;

    // Constructor
    public Video(String title) {
        this.title = title;
        this.checkedOut = false;
        this.totalRating = 0;
        this.ratingCount = 0;
    }

    // Method to check out the video
    public void checkOut() {
        if (!checkedOut) {
            checkedOut = true;
            System.out.println(title + " has been checked out.");
        } else {
            System.out.println(title + " is already checked out.");
        }
    }

    // Method to return the video
    public void returnVideo() {
        if (checkedOut) {
            checkedOut = false;
            System.out.println(title + " has been returned.");
        } else {
            System.out.println(title + " was not checked out.");
        }
    }

    // Method to receive a rating
    public void receiveRating(int rating) {
        if (rating >= 1 && rating <= 5) {
            totalRating += rating;
            ratingCount++;
        } else {
            System.out.println("Invalid rating. Please enter a rating between 1 and 5.");
        }
    }

    // Method to get the average rating
    public double getAverageRating() {
        return ratingCount == 0 ? 0 : totalRating / ratingCount;
    }

    // Method to check if video is checked out
    public boolean isCheckedOut() {
        return checkedOut;
    }

    // Method to get video title
    public String getTitle() {
        return title;
    }

    // Method to print video details
    @Override
    public String toString() {
        return "Title: " + title + " | Checked Out: " + checkedOut + " | Average Rating: " + getAverageRating();
    }
}

// VideoStore class
class VideoStore {
    private Video[] inventory;
    private int count;

    // Constructor
    public VideoStore() {
        inventory = new Video[10]; // Array of length 10
        count = 0;
    }

    // Method to add a video
    public void addVideo(String title) {
        if (count < inventory.length) {
            inventory[count] = new Video(title);
            count++;
            System.out.println(title + " added to inventory.");
        } else {
            System.out.println("Inventory full, cannot add more videos.");
        }
    }

    // Method to check out a video by title
    public void checkOut(String title) {
        for (int i = 0; i < count; i++) {
            if (inventory[i].getTitle().equalsIgnoreCase(title)) {
                inventory[i].checkOut();
                return;
            }
        }
        System.out.println("Video not found in inventory.");
    }

    // Method to return a video by title
    public void returnVideo(String title) {
        for (int i = 0; i < count; i++) {
            if (inventory[i].getTitle().equalsIgnoreCase(title)) {
                inventory[i].returnVideo();
                return;
            }
        }
        System.out.println("Video not found in inventory.");
    }

    // Method to receive a rating for a video
    public void receiveRating(String title, int rating) {
        for (int i = 0; i < count; i++) {
            if (inventory[i].getTitle().equalsIgnoreCase(title)) {
                inventory[i].receiveRating(rating);
                System.out.println("Rating " + rating + " received for " + title);
                return;
            }
        }
        System.out.println("Video not found in inventory.");
    }

    public void listInventory() {
        System.out.println("\nVideo Store Inventory:");
        for (int i = 0; i < count; i++) {
            System.out.println(inventory[i]);
        }
    }
}

// VideoStoreLauncher class (Main class)
public class VideoStoreLauncher {
    public static void main(String[] args) {
        VideoStore store = new VideoStore();

        // Adding 5 videos to the store
        store.addVideo("Barfi");
        store.addVideo("Rockstar");
        store.addVideo("Wake up sid");
        store.addVideo("YJHD");
        store.addVideo("Ajab prem Ki gajab kahani");

        store.receiveRating("Barfi", 5);
        store.receiveRating("Rockstar", 4);
        store.receiveRating("Wake up sid", 5);
        store.receiveRating("YJHD", 4);
        store.receiveRating("Ajab prem Ki gajab kahani", 3);

        store.checkOut("Barfi");
        store.checkOut("Rockstar");
        store.checkOut("Wake up sid");
        store.checkOut("YJHD");
        store.checkOut("Ajab prem Ki gajab kahani");

        // Returning each video
        store.returnVideo("Barfi");
        store.returnVideo("Rockstar");
        store.returnVideo("Wake up sid");
        store.returnVideo("YJHD");
        store.returnVideo("Ajab prem Ki gajab kahani");

        // Renting out "Wake up sid" again
        store.checkOut("Wake up sid");

        // Listing the inventory
        store.listInventory();
    }
}

