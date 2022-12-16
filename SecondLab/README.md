
##### Computers architecture Lab 2


####  Chaitidis Dimitrios (AEM: 9310)


#### email: chaitidi@ece.auth.gr



Στην αρχή της εργασίας μας ζητήθηκε να τρέξουμε μεμονομένα τις παρακάτων εντολές.

./build/ARM/gem5.opt -d spec_results/specbzip configs/example/se.py --cputype=MinorCPU --caches --l2cache -c spec_cpu2006/401.bzip2/src/specbzip -o "spec_cpu2006/401.bzip2/data/input.program 10" -I 100000000

./build/ARM/gem5.opt -d spec_results/specmcf configs/example/se.py --cputype=MinorCPU --caches --l2cache -c spec_cpu2006/429.mcf/src/specmcf -o "spec_cpu2006/429.mcf/data/inp.in" -I 100000000

./build/ARM/gem5.opt -d spec_results/spechmmer configs/example/se.py --cputype=MinorCPU --caches --l2cache -c spec_cpu2006/456.hmmer/src/spechmmer -o "-- fixed 0 --mean 325 --num 45000 --sd 200 --seed 0 spec_cpu2006/456.hmmer/data/bombesin.hmm" -I 100000000

 ./build/ARM/gem5.opt -d spec_results/specsjeng configs/example/se.py --cputype=MinorCPU --caches --l2cache -c spec_cpu2006/458.sjeng/src/specsjeng -o
"spec_cpu2006/458.sjeng/data/test.txt" -I 100000000

 ./build/ARM/gem5.opt -d spec_results/speclibm configs/example/se.py --cputype=MinorCPU --caches --l2cache -c spec_cpu2006/470.lbm/src/speclibm -o "20
spec_cpu2006/470.lbm/data/lbm.in 0 1 spec_cpu2006/470.lbm/data/100_100_130_cf_a.of" -I 100000000











Αφού έχουμε τρέξει μεμονομένα τις εντολές που μας δόθηκαν προχωρούμε στο επόμενο ερώτημα.
Το μέγεθος της L1 instruction, L1 Data caches και της L2 caches.Το associativity κάθε μίας από αυτές και το μέγεθος της cache line
Τα μεγέθη αυτά είναι ίδια για όλα τα Benchmarks
Από τα αρχεία config.ini του φακέλου spec_results για κάθε ένα από τα specbzip, spechmmer, speclibm, specmcf, specsjeng παρατηρούμε τα εξής μεγέθη:


Dcache_size & associativity

assoc=2
size=65536

Icache_size & associativity

assoc=2
size=32768



L2_cache_size & associativity

assoc=8
size=2097152

Cache_line_size 

cache line size:64B



Από τα αρχεία stats.txt του φακέλου spec_results για κάθε ένα από τα specbzip, spechmmer, speclibm, specmcf, specsjeng παρατηρούμε τα παρακάτω αποτελέσματα:


Για το αρχείο specbzip

sim_seconds                                  0.083982                       # Number of seconds simulated

system.cpu.cpi                               1.679650                       # CPI: cycles per instruction

system.cpu.icache.overall_miss_rate::total   0.000077                       # miss rate for overall accesses

system.cpu.dcache.overall_miss_rate::total   0.014798                       # miss rate for overall accesses

system.l2.overall_miss_rate::total           0.282163                       # miss rate for overall accesses





Για το αρχείο spechmmer

sim_seconds                                  0.059396                       # Number of seconds simulated

system.cpu.cpi                               1.187917                       # CPI: cycles per instruction

system.cpu.icache.overall_miss_rate::total   0.000221                       # miss rate for overall accesses

system.cpu.dcache.overall_miss_rate::total   0.001637                       # miss rate for overall accesses

system.l2.overall_miss_rate::total           0.077760                       # miss rate for overall accesses





Για το αρχειο speclibm

sim_seconds                                  0.000045                       # Number of seconds simulated

system.cpu.cpi                               8.032258                       # CPI: cycles per instruction

system.cpu.icache.overall_miss_rate::total   0.094160                       # miss rate for overall accesses

system.cpu.dcache.overall_miss_rate::total   0.063140                       # miss rate for overall accesses

system.l2.overall_miss_rate::total           0.926230                       # miss rate for overall accesses




Για το αρχείο specmcf

sim_seconds                                  0.064955                       # Number of seconds simulated

system.cpu.cpi                               1.299095                       # CPI: cycles per instruction

system.cpu.icache.overall_miss_rate::total   0.023612                       # miss rate for overall accesses

system.cpu.dcache.overall_miss_rate::total   0.002108                       # miss rate for overall accesses

system.l2.overall_miss_rate::total           0.055046                       # miss rate for overall accesses



Για το αρχείο specsjeng

sim_seconds                                 0.513528                       # Number of seconds simulated

system.cpu.cpi                              10.270554                      # CPI: cycles per instruction

system.cpu.icache.overall_miss_rate::total  0.000020                       # miss rate for overall accesses

system.cpu.dcache.overall_miss_rate::total  0.121831                       # miss rate for overall accesses

system.l2.overall_miss_rate::total          0.999972                       # miss rate for overall accesses



Γενικότερα παρατηρούμε ότι όσο αυξάνονται τα miss rates απο το εκάστοτε Benchmark, τότε αυξάνεται και το CPI που είναι λογικό καθώς σε περίπτωση 
που δεν βρεί κάτι (miss rate) τότε θα χρειαστεί περισσότερο χρόνο να το βρεί. Ετσι καταλήγουμε να έχουμε μεγαλύτερο CPI (cycles per instruction).

 system.clk_domain.clock                          1000                       # Clock period in ticks
 system.cpu_clk_domain.clock                      1000                       # Clock period in ticks



Η εργασία αυτή αρχικά ήταν ιδιαίτερα πιο απαιτητική και χρονοβόρα απο την προηγούμενη. Απαιτούσε πολύ περισσότερες γνώσεις τόσο για τον gem5 όσο και για το λειτουργικό που χρησιμοποιούμε.
Προσωπικά δυσκολεύτηκα ιδιαίτερα πολύ για το κομμάτι που απαιτούσε την αυτοματοποίηση της εκτέλεσης των εντολών. Λόγω των προβλημάτων που συνάντησα δυστηχώς δεν μπόρεσα 
να αφιερώσω επαρκή χρόνο στην "θεωρία" που χρειαζόταν για την εύρεση των καλύτερων "specs", ουσιαστικά να πληρείται η προυπόθεση του ερωτήματος "Ως μέγιστη απόδοση θεωρούμε το ελάχιστο CPI (όσο πιο κοντά στο 1 μπορεί να φτάσει)". 
