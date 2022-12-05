# ComputerArchitecture
__Lab Computer Architecture__

__Δημήτριος Χαϊτίδης (Dimitrios Chaitidis) (ΑΕΜ: 9310)__

__Email__: chaitidi@ece.auth.gr

Στο πρώτο εργαστήριο κλιθήκαμε να εγκαταστήσουμε το Gem5 μέσω ενός λογισμικού που δουλεύει παράλληλα με το λογισμικό του υπολογιστή μας. Συγκεκριμένα στον υπολογιστή μας που δουλεύει με windows να τρέξουμε Linux. Η διαδικασία αυτή επιτυγχάνεται μέσω ενος Virtual Box Machine. Επι της ουσίας δημιουργείται ενα περιβάλλον εργασίας εντός του τρέχοντος λογισμικού (windows) και εκεί χρησιμοποιούμαι το επιθυμητό λογισμικό (Linux). 
Στο περιβάλλον εργασίας αυτό (Linux) πειραματιζόμαστε με το Gem5. Ο Gem5 μας επιτρέπει να δοκιμάσουμε διάφορους πειραματισμούς σε ότι αφορά την αρχιτεκτονική του υπολογιστή μας. Προσφέρει πληροφορίες για την αρχιτεκτονική του υπολογιστή για την οποία χρησιμοποιήσαμε για να τρέξουμε το εκάστοτε πρόγραμμα.
Στην πρώτο μέρος της εργασίας , κλιθήκαμε να τρέξουμε ενα απλό πρόγραμμα, το Hello world!. Τρέχοντας την εντολή :

./build/ARM/gem5.opt configs/example/arm/starter_se.py --cpu='minor' "tests/test-progs/hello/bin/arm/linux/hello" # Hello world!

###### Ερώτημα 1.

Ανοίγωντας το file starter_se.py βλέπουμε μερικά βασικά χαρακτηριστικά.

-__CPU__ : parser.add_argument("--cpu-freq", type=str, default="1GHz")

-__Caches__: cpu_types = {
    "atomic" : ( AtomicSimpleCPU, None, None, None, None),
    "minor" : (MinorCPU,
               devices.L1I, devices.L1D,
               devices.WalkCache,
               devices.L2),
    "hpi" : ( HPI.HPI,
              HPI.HPI_ICache, HPI.HPI_DCache,
              HPI.HPI_WalkCache,
              HPI.HPI_L2)
}
Ωστόσο γνωρίζουμε απο την εντολή που δώσαμε οτι η CPU που χρησιμοποιήθηε είναι η 'minor'

-__Μνήμη__ :parser.add_argument("--mem-type", default="DDR3_1600_8x8",
                        choices=ObjectList.mem_list.get_names(),
                        help = "type of memory to use")




###### Ερώτημα 2.

Ανοίγωντας το αρχείο config.json config.ini παρατηρούμε οτι μας παρέχονται πληροφορίες  για το σύστημα που εξομοιώνει ο Gem5 . Επίσης χρησιμοποιώντας το αρχέιο stats.txt μπορούμε να δούμε για τις παρακάτω εντολές το αποτέλεσμα τους και την σημασία τους (δηλαδή τι απεικονίζει η καθε μία) :

-__sim_seconds__ :   0.000035 # Number of seconds simulated

-__sim_insts__:      5027     # Number of instructions simulated

-__host_inst_rate__: 34489    # Simulator instruction rate (inst/s)

-__commited instructions__: system.cpu_cluster.cpus.committedInsts  5027   # Number of instructions committed

-__L2 cache__: system.cpu_cluster.l2.demand_accesses::.cpu_cluster.cpus.inst  327     # number of demand (read+write) accesses


Στην εργασία αυτή επίσης μας ζητήθηλε να αναζητήσουμε πληροφορίες για τους in-order cpu's που χρησιμοποιούμαι στον Gem5. 
Αναζητώντας πληροφορίες στο gem5.org βρίσκουμε τις εξής πληροφορίες: 

https://www.gem5.org/documentation/general_docs/cpu_models/SimpleCPU

BaseCPU
BaseSimpleCPU
AtomicSimpleCPU
TimingSimpleCPU
MinorO3CPU
MinorCPU


###### Ερώτημα 3.

Γνωρίζουμε οτι οι 2 κύριες CPU που χρησιμοποιούνται είναι οι AtomicSimpleCPU, TimingSimpleCPU . Οπου οι 2 τελευταίες παράγονται ουσιαστικά απο την BaseSimpleCPU.
H MinorO3CPU δεν χρησιμοποιείται καθως είναι out of order.
Και φυσικά όπως και χρησιμοποιήσαμε στο παράδειγμα μας υπάρχει η MinorCPU.
Για τον BaseSimpleCPU μαθαίνουμε τα εξής:
Είναι απλή abstract CPU χωρίς pipeline. Συνεπαγωγικά είναι μη ρεαλιστική αλλα παράλληλα είναι πολύ γρήγορη. Είναι ουσιαστικά ενας εναλλακτικός τρόπος για να κάνει fast forwarding boot κατα την λειτουργία τους.
Για τον __AtomicSimpleCPU__:
Είναι το προεπιλεγμένο μοντέλο επεξεργαστή με ακαριαία προσπέλαση μνήμης. Ωστόσο επίσης δεν είναι ρεαλιστικός.
__MinorCPU__ : 
Αποτελεί ένα in-order μοντέλο με προκαθορισμένη διαδικασία διοχέτευσης αλλά προσαρμοζόμενες δομές δεδομένων και προσαρμοζόμενη συμπεριφορά εκτέλεσης.Το σταθερό pipeline του βοηθάει στην αναγνώριση και οπτικοποίηση μέσα σε αυτό της κάθε εντολής από μια προσομοίωση.
Για τον __TimingSimpleCPU__:
Οι προσπελάσεις μνήμης είναι ρεαλιστικές αλλα ο επεξεργαστής δεν έχει pipeline. Η προσομοίωση είναι γρήγορη αλλά πιο αργή από τον AtomicSimpleCPU. Οι Caches κάνουν μεγάλη διαφορά και οδηγούν σε γρηγορότερους χρόνους προσπέλασης μνήμης.



###### 3a)
Το Script που έτρεξα στον gem5 αφού το έκανα static compile, είναι απλό καθώς μας δόθηκε η "παρατήρηση" να μην γράψουμε κάποιο απαιτητικό πρόγραμμα καθώς θα έππερνε πολύ περισσότερο χρόνο στην εκτέλεση του στον gem5, είναι το εξής:

#include <stdio.h>

int main(){


        int num1 = 230 , num2 = 11 , sum = 0, t1 = 0, t2 = 1, nextTerm;

        for(int i=0;i<10000;i++){

                //calculate sum
                sum = sum + num1 * i + num2 * i * 2* sum /1000;
                sum=sum*sum*sum/5642;
                for (int k=0; k<5; k++){
                        sum=k*sum+1;

                }

        }


        printf("Result is %d", sum);

        return 0;
}


Στην πρώτη φορά που το έτρεξα χρησιμοποίησα την MinorCPU και στην συνέχεια την TimingSimpleCPU . Μας ζητήθηκε να παραθέσουμε τους χρόνους εκτέλεσης οι οποίοι φαίνονται στο παρακάτω πίνακα

|                     | C script     |
| :-----------------: | ------------ |
|    **MinorCPU**     | 0.000655 sec |
| **TimingSimpleCPU** | 0.001569 sec |

###### 3b.
Η διαφορά στους χρόνους οφείλεται στις απανωτές προσπελάσεις στη μνήμη που περιλαμβάνει το προγράμμα. H *pipelined* λογική του *MinorCPU* μοντέλου υπερτερεί έναντι του *TimingSimpleCPU* , ο οποίος μπλοκάρει την εκτέλεση περιμένοντας το αποτέλεσμα της προσπέλασης της μνήμης.

###### 3c.

###### Αρχικά άλλαξα το *cpu_clock*

|                     | 1GHz         | 2GHz         | 3GHz         |
| :-----------------: | ------------ | ------------ | ------------ |
|    **MinorCPU**     | 0.001282 sec | 0.000655 sec | 0.000446 sec |
| **TimingSimpleCPU** | 0.003113 sec | 0.001569 sec | 0.001054 sec |

Παρατηρήσαμε ότι υπάρχει μεγάλη μείωση στους χρόνους εκτέλεσης, και στις 2 περιπτώσεις. Φυσικά αυτό ήταν αναμενόμενο.


###### Μετά δοκίμασα να αλλάξω το *--mem-type*

|                     |  HBM_1000_4H_1x64   | DDR3_1600    | DDR4_2400_16x4   |
| :-----------------: | ------------------- | ------------ | ---------------- |
|    **MinorCPU**     | 0.000661 sec        | 0.000655 sec | 0.000654 sec     |
| **TimingSimpleCPU** | 0.003118 sec        | 0.001569 sec | 0.003112 sec     |

Στην προκειμένη περίπτωση οι αλλαγές στον χρόνο εκτέλεσης, με τις αλλαγές που χρησιμοποιήσαμε για τον τύπο της μνήμης, δεν είναι ξεκάθαρες. Προφανώς αυτό οφείλεται στην "φύση" του προγράμματος (script) που υλοποιήσαμε και στην απλότητα του.




#### __Συνολικά__: 
Η εργασία αυτή για το πρώτο εργαστήριο του μαθήματος μας εξοικίωσε με την χρήση ενός ακόμα λειτουργικου συστήματος στο ήδη υπάρχον λειτουργικό σύστημα μας.
Επίσης εξοικιωθηκαμε με τον Gem5 , ενα εξαιρετικό εργαλείο για την επιστήμη της Αρχιτεκτονικής των Υπολογιστών. Δοκιμάσαμε να τρέξουμε "προγράμματα" και να δούμε τα αποτελέσματα απο διάφορες μετρικές που μας ενδιαφέρουν ενώ παράλληλα μάθαμε διαφορες πληροφιές για τα διαφορετικά μοντέλα επεξεργαστών που υποστηρίζει ο Gem5 και στοιχεία/πληροφορίες για αυτούς. Προσωπικά μου άρεσε ιδιαίτερα που έτρεξα ενα script δικής μου υλοποίησης και έβλεπα καθώς άλλαζα την πολυπλοκότητα του, τα διάφορα αποτελέσματα απο τις μετρικές που μας ενδιαφέρουν.
Ωστόσο θεωρώ πως ακόμη έχουμε δει μονάχα την κορυφή απο το βουνό που λέγεται Gem5. Ανυπομονώ (επιφυλακτικά) για τις προσεχόμενες εργασίες.
