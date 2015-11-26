# ITB-Racer-1.0
/*Java program about race using array*/
mport java.util.Scanner;
public class ITBRacer {
	public static String[] names; //array of names
	public static double[] times; //array of times
	public static int racesTot;

	/**
	 * Main routine
	 */
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		String input = "";
		racesTot = 0;
		int globalCount = 0;
		double time;

		// Get the number of races
		System.out.println("Welcome to Racer 1.0. Please choose an option");

		while (racesTot == 0) {
			System.out.print("Insert the number of races: ");
			input = scanner.nextLine();

			// avoid number format exception.
			try {
				racesTot = Integer.parseInt(input);
				if (racesTot < 2 || racesTot > 12) {
					System.out.println("There must be between 2 and 12 racers");
					racesTot = 0;
				}
				names = new String[racesTot];
				times = new double[racesTot];

			} catch (NumberFormatException e) {
				System.out.println("Number of races must be a number");
			}
		}

		// for each racer, input the name and time
		for(globalCount = 0; globalCount < racesTot; globalCount++) {
			input = "";

			while (input.length() == 0) {
				System.out.print("Please insert a name for racer "+(globalCount+1)+": ");

				input = scanner.nextLine();

				if (input.length() > 0) {
					names[globalCount] = input;
				} else
					System.out.println("Name cannot be blanck");
			}

			input = "";
			while (input.length() == 0) {
				System.out.print("Enter a time for the racer "+names[globalCount]+": ");
				input = scanner.nextLine();

				// avoid number format exception.
				try {
					time = Double.parseDouble(input);
					if (time > 0 && time <= 5) {
						times[globalCount] = time;
					} else {
						System.out.println( "Time must be between 0.0 and 5.0 minutes");
						input = "";
					}

				} catch (NumberFormatException e) {
					System.out.println("Time must be a number.");
					input = "";
				}
			}
		}

		// bring the options to show statistics, search racer or exit program
		while (true) {
			System.out.println("=============================================================================");
		    System.out.println("Type 'show' to show statistics");
		    System.out.println("Type 'search' to search for a racer");
		    System.out.println("Type 'exit' to exit program");
		    System.out.print("Command: ");

		    input = scanner.nextLine();
		    input = input.toLowerCase();

		    if (input.equals("exit")) {
		    	break;
		    } else if (input.equals("search")) {
		    	System.out.print("Name of the racer: ");

			    input = scanner.nextLine();

		    	int pos = searchRacer(input);
		    	System.out.println("=============================================================================");
		    	if (pos >= 0)
		    		System.out.println("Racer "+nameAtPosition(pos)+" placed "+(racesTot - pos )+" with time "+String.valueOf(timeAtPosition(pos))+" minutes");
		    	else
		    		System.out.println("Racer "+input+" not found");
		    } else if (input.equals("show")) {
		    	showAll();
		    }
		}

	}

	/**
	 * Method that returns the average time of races
	 */
	public static double avgRaceTimes() {
		double avg = 0;
		double sum = 0;

		for (int i = 0; i < racesTot; i++) {
			sum = sum + times[i];
		}

		avg = sum / racesTot;

		return avg;
	}

	/**
	 * Method that shows the statistics for the races
	 */
	public static void showAll() {
		System.out.println("=============================================================================");
    	System.out.println("Avarage race competition time: "+Double.toString(avgRaceTimes())+" minutes.");
    	sortDescending();
    	System.out.println("Fastest racer "+nameAtPosition(racesTot - 1)+" time "+String.valueOf(timeAtPosition(racesTot - 1)+" min"));
    	System.out.println("Slowest racer "+nameAtPosition(0)+" time "+String.valueOf(timeAtPosition(0)+" min"));
    	System.out.println("=============================================================================");
    	System.out.println("All racers:");
    	for (int i = 0; i < racesTot; i++) {
			System.out.println(racesTot-i+" Position: Racer "+names[i]+" with time "+times[i]+" minutes");
		}
	}

	/**
	 * Method that sort the races in order descending
	 */
	public static void sortDescending() {
		for (int i = 0; i < racesTot; i++) {
			for (int j = 0; j < racesTot; j++) {
				if (times[i] > times[j]) {
					double auxTime = times[j];
					String auxName = names[j];

					times[j] = times[i];
					times[i] = auxTime;
					names[j] = names[i];
					names[i] = auxName;
				}
			}
		}
	}

	/**
	 * Method that returns the position of the giving racer
	 */
	public static int searchRacer(String name) {
		int pos = -1;

		for (int i = 0; i < racesTot; i++) {
			if (names[i].equals(name))
				pos = i;
		}

		return pos;
	}

	/**
	 * Method that return the name of the racer at the giving position
	 */
	public static String nameAtPosition(int position) {
		return names[position];
	}

	/**
	 * Method that return the time of the racer at the giving position
	 */
	public static double timeAtPosition(int position) {
		return
		times[position];
	}

}
