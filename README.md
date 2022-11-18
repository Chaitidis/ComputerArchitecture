# ComputerArchitecture
Lab Computer Architecture

Στο πρώτο εργαστήριο κλιθήκαμε να εγκαταστήσουμε το Gem5 μέσω ενός λογισμικού που δουλεύει παράλληλα με το λογισμικό του υπολογιστή μας. Συγκεκριμένα στον υπολογιστή μας που δουλεύει με windows να τρέξουμε Linux. Η διαδικασία αυτή επιτυγχάνεται μέσω ενος Virtual Box Machine. Επι της ουσίας δημιουργείται ενα περιβάλλον εργασίας εντός του τρέχοντος λογισμικού (windows) και εκεί χρησιμοποιούμαι το επιθυμητό λογισμικό (Linux). 
Στο περιβάλλον εργασίας αυτό (Linux) πειραματιζόμαστε με το Gem5. Ο Gem5 μας επιτρέπει να δοκιμάσουμε διάφορους πειραματισμούς σε ότι αφορά την αρχιτεκτονική του υπολογιστή μας. Προσφέρει πληροφορίες για την αρχιτεκτονική του υπολογιστή για την οποία χρησιμοποιήσαμε για να τρέξουμε το εκάστοτε πρόγραμμα.
Στην πρώτη εργασία , κλιθήκαμε να τρέξουμε ενα απλό πρόγραμμα, το Hello world!. Τρέχοντας την εντολή :
./build/ARM/gem5.opt configs/example/arm/starter_se.py --cpu='minor' "tests/test-progs/hello/bin/arm/linux/hello" # Hello world!
Ανοίγωντας το file starter_se.py που χρησιμοποιήθηκε για την εκτέλεση του Hello world βλέπουμε μερικά βασικά χαρακτηριστικά.
CPU : parser.add_argument("--cpu-freq", type=str, default="1GHz")

Caches: cpu_types = {
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

Μνήμη :parser.add_argument("--mem-type", default="DDR3_1600_8x8",
                        choices=ObjectList.mem_list.get_names(),
                        help = "type of memory to use")

Συχνότητα λειτουργίας :

Βασικές μονάδες :


Ανοίγωντας το αρχείο config.json config.ini παρατηρούμε οτι μας παρέχονται πληροφορίες  για το σύστημα που εξομοιώνει ο Gem5 . Επίσης χρησιμοποιώντας το αρχέιο stats.txt μπορούμε να δούμε για τις παρακάτω εντολές το αποτέλεσμα τους και την σημασία τους (δηλαδή τι απεικονίζει η καθε μία) :

sim_seconds :   0.000035 # Number of seconds simulated

sim_insts:      5027     # Number of instructions simulated

host_inst_rate: 34489    # Simulator instruction rate (inst/s)

commited instructions: system.cpu_cluster.cpus.committedInsts  5027   # Number of instructions committed

L2 cache: system.cpu_cluster.l2.demand_accesses::.cpu_cluster.cpus.inst  327     # number of demand (read+write) accesses
