# ComputerArchitecture
__Lab Computer Architecture__

__Δημήτριος Χαϊτίδης (Dimitrios Chaitidis) (ΑΕΜ: 9310)__

__Email__: chaitidi@ece.auth.gr



##### __Βήμα 1__


###### __Ερώτημα 1__



Η διοχέτευση ισχύος ταξινομείται σε δύο κατηγορίες: 

 1. __Static power (leakage power) dissipation__
 
 2. __Dynamic power dissipation__

Το άθροισμα της συνολικής διοχέτευσης ισχύος ισούται με το άθροισμα των δύο παρπάνω παραγόντων.

__Static power dissipation__
Είναι η διοχέτευση ισχύος με τη μορφή ρεύματος διαρροής όταν το σύστημα δεν τροφοδοτείται η βρίσκεται σε standby mode. 
Η διοχέτευση ισχύος είναι ανεξάρτητη της συχνότητας και του "switching" του συστήματος. Η στατική ισχύ καταναλώνεται λόγω της διαρροής ρεύματος μέσω των τρανσίστορ. Υπάρχουν δύο είδη διαρροών και το μέγεθος κάθε ρεύματος διαρροής είναι ανάλογο με το πλάτος των τρανσίστορ και εξαρτάται από την λογική κατάσταση τους.Όταν η τάση πύλης (gate voltage) είναι μικρότερη από την τάση κατωφλίου (threshold voltage) προκύπτει το πρώτο είδος διαρροής, η διαρροή κατωφλίου (subthreshold leakage), συγκεκριμένα όταν ένα τρανσίστορ το οποίο είναι φαινομενικά στην κατάσταση off αφήνει ένα μικρό ρεύμα να περάσει ανάμεσα στην πηγή (source) και την εκροή (drain). Ο τύπος για να υπολογίσουμε το ρεύμα που δημιουργεί την τάση subthreshold είναι ο παρακάτω : 

 **Isub-threshold=μo*Cox*W/(L*V^2*e^1.8*e^[(Vgs-Vth)/ηVth]**
 
Ένα σημαντικό σημείο σε αυτόν τον τύπο είναι ότι το ρεύμα sub-threshold είναι εκθετικά ανάλογο του (Vgs-Vth). Κανονικά η τάση κατωφλίου (Vth) είναι έιναι αρκετά μεγάλη ώστε όταν η τάση Vgs ισούται με 0 το ρεύμα sub-threshold είναι πολύ μικρό. Ωστόσο με τις σημερινές μικρότερες γεωμετρίες και την μείωση στην τάση τροφοδοσίας, η Vth πρέπει επίσης να μειωθεί, με αποτέλεσμα η διαρροή ρεύματος που προκύπτει όταν η Vgs=0 είναι πλεον σημαντική. Από τον τύπο φαίνεται ότι μπορούμε να μειώσουμε το ρεύμα sub-threshold αυξάνοντας την Vth ή μειώνοντας την Vgs. Ωστόσο αυξάνοντας την Vth επηρεάζεται η επίδοση, για αυτό υπάρχει ένα μεγάλο "πάρε-δώσε" μεταξύ επιδόσεων και κατανάλωσης ισχύος στην διαδικασία σχεδίασης. Ο δεύτερος τύπος διαρροής ονομάζεται διαρροή πηγής (gate leakage) και είναι το ρεύμα που ρέει μέσω της πηγής.

__Dynamic power dissipation__
Οφείλεται σε δύο παράγοντες , την switching ισχύ και την short-circuit ισχύ.
Η πρώτη διοχετεύεται όταν φορτίζονται και ξεφορτίζονται οι χωρητικότητες του συστήματος. Κατά τη φόρτιση του πυκνωτή CL μέσω του pmos transistor η τάση του ανεβαίνει από το 0 στο Vdd και ένα συγκεκριμένο ποσό ενέργειας αντλείται από το τροφοδοτικό. Μέρος της ενέργειας αυτής διοχετεύεται στη pmos συσκευή και η υπόλοιπη αποθηκεύεται στον πυκνωτή.Η ίδια διαδικασία ισχύει και κατά την αποφόρτιση(nmos).
Η δεύτερη ειναι η ισχύς που διοχετεύται όταν η πύλη των transistor αλλάζει κατάσταση. Για ένα μικρό χρονικο διάστημα t δημιουργείται ένα βραχυκύκλωμα μεταξύ της παροχής τάσης και της γείωσης κατά τη διάρκεια του οποίου και οι δυο συσκευές είναι στο ON (nmos, pmos).

Όταν τρέχουμε διαφορετικά προγράμματα στον ίδιο επεξεργαστή η leakage power δεν αλλάζει καθώς εξαρτάται μόνο από την τεχνολογία του επεξεργαστή. Αυτό που αλλάζει είναι η dynamic power (δυναμική ισχύς) επειδή αλλάζει η switching activity και επομένως η switching frequency.
Όταν ένα πρόγραμμα αυξάνεται χρονικά, αυξάνεται και οι switching activity και switching frequency. Άρα αυξάνεται και η δυναμική ισχύς που καταναλώνεται.


###### __Ερώτημα 2__

Έστω ότι έχουμε ένα σύστημα με μπαταρία συγκεκριμένης χωρητικότητας και οι δύο επεξεργαστές καταναλώνουν 5 Watt και 50 Watt αντίστοιχα. Αν ο δεύτερος επεξεργαστής εκτελεί τα προγράμματα σε ταχύτερο χρόνο από τον πρώτο και μείνει σε "ανενεργή λειτουργία" (Idle time), μπορεί να δώσει καλύτερα αποτελέσματα όσον αφορά την ενέργεια ( *energy_efficiency* ). 

Ο McPAT είναι ένας emulator ο οποίος σύμφωνα με τα χαρακτηριστικά και τις παραμέτρους μιας αρχιτεκτονικής επεξεργαστή επιστρέφει αποτελέσματα σχετικά με τη κατανάλωση ισχύος , την γεωμετρία του cpu κ.α.
Αυτό πού δεν μπορεί να επιστρέψει είναι ο χρόνος εκτέλεσης ενός προγράμματος ή το idle_time του cpu όταν εκτελείται το πρόγραμμα. Αυτός είναι ο λόγος που δε μπορεί να δώσει επαρκείς πληροφορίες για το ερώτημα μας.
Συνεπαγωγικά αυτό που θα χρειαζόμασταν θα ήταν να μας προσφέρει σαν πληροφορίες τον χρόνο εκτέλεσης του προγράμματος (cpi time) και τον ανενεργό χρόνο του (idle time).



######  __Ερώτημα 3__ 

<table>
<thead>
<tr>
<th>Processors</th>
<th>Technology</th>
<th>Core clockrate</th>
<th>Total Leakage</th>
<th>Peak Dynamic</th>
<th>Total Power Consumption</th>
</tr>
</thead>
<tbody>
<tr>
<td>XEON</td>
<td>65nm</td>
<td>3400MHz</td>
<td>36.8319 W</td>
<td>98.1063 W</td>
<td>134.938 W</td>
</tr>
<tr>
<td>ARM A9</td>
<td>40nm</td>
<td>2000MHz</td>
<td>0.108687 W</td>
<td>1.6332 W</td>
<td>1.74189 W</td>
</tr>
</tbody>
</table>

Η συνολική κατανάλωση ισχύος του *ARM A9* ισούται με 1.74189 W. Υποθέτοντας ότι ο XEON είναι 50 φορές ταχύτερος τότε ο ARM θα καταναλώνει κατά τη διάρκεια εκτέλεσης του προγράμματος 50 * 1.74189 W = 87.0945 W < 134.938 W. Ακόμη κι αν ο XEON μένει idle το υπόλοιπο χρονικό διάστημα ο ARM είναι περισσότερο energy efficient από τον XEON.



##### __Βιβλιογραφία__ :
https://www.einfochips.com/blog/power-dissipation-in-vlsi-moving-to-low-power-soc-design-while-improving-performance/
(https://github.com/HewlettPackard/mcpat)  


#### __Συνολικά__: 

Η 3η εργαστηριακή άσκηση στην Αρχιτεκτονική των υπολογιστών αναμενόταν εξαιρετικά δύσκολη. Ωστόσο πολύ γρήγορα αποδείχθηκε το αντίθετο. Το 1ο βήμα κατα κύριο λόγο απαιτούσε αναζήτηση πληροφοριών κάτι το οποίο μας εμπλούτισε σχετικά με τις γενικότερες γνώσεις μας απέναντι στην επιστήμη της Αρχιτεκτονικής των υπολογιστών. Προσωπικά οι δυσκολίες που αντιμετώπισα ήταν κατα κύριο λόγο στο δεύτερο εργαστήριο. Ο όγκος των δεδομένων που αντιμετώπισα ήταν ιδιαίτερα μεγάλος και ατομικά ήταν πολύ πιο δύσκολο να το διαχειριστώ. Γενικότερα τα εργαστήρια της αρχιτεκτονικής των υπολογιστών, ήταν εργαστήρια στα οποία κάθε μέλος της ομάδας μπορύσε να ήταν "hands on" , κάτι το οποίο υπο τις κατάλληλες συνθήκες θα ήταν ιδιαίτερα ευνοϊκό.
