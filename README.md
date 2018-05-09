# Data visualisation

## Δρουγκάνη Ανθή

## Π2014104

Αποθετήριο Μαθήματος: https://github.com/anthidrougani/sw
Αποθετήριο κώδικα: https://github.com/anthidrougani/D3js-uk-political-donations/tree/gh-pages

Τελική Αναφορά 

Επέλεξα την εργασία οπτικοποίησης δεδομένων χορηγιών  (uk) , πάνω στο μάθημα τεχνολογία λογισμικού του στ εξαμήνου . έκανα όλες τις αλλαγές που ζητούνται από το πρώτο παραδοτέο 
Μετατροπή του full-viz.html σε index.html ώστε να μην καταλήγει το url σε full-viz.html

Αλλαγή χρωμάτων στις μπάλες με τα δεδομένα, καθώς και στα αντίστοιχα 3 πεδία της ομαδοποίησης Split by party στο style.css

![1](https://user-images.githubusercontent.com/22959040/39838710-c74e2f0e-53e2-11e8-9746-b7478b0f94d8.jpg)

Αλλαγή ώστε να ακούγεται ήχος κάθε φορά που ο χρήστης της εφαρμογής κάνει κλικ σε μία από τις επιλογές/κουμπιά ομαδοποίησης των δεδομένων στο index.html

var  sound = new Audio("click.mp3");
<li><a href="#" role="button" class="pure-button switch" id="all-donations"onmousedown="sound.play()">All money</a>
	            </li>
	            <li><a href="#" role="button" class="pure-button switch" id="group-by-money-source"onmousedown="sound.play()">The public's purse</a>
	            </li>
	            <li><a href="#" role="button" class="pure-button switch" id="group-by-party"onmousedown="sound.play()">Split by party</a>
	            </li>
	            <li><a href="#" role="button" class="pure-button switch" id="group-by-donor-type"onmousedown="sound.play()">Split by type of donor</a>
	            </li>



Αλλαγή ώστε όταν το ποντίκι βρίσκεται μέσα στον κύκλο κάποιου δωρητή, να ακούγεται η ονομασία του δωρητή και το ποσό της δωρεάς στο chart.js

var speech = new SpeechSynthesisUtterance("Donation by " + donor + ". It amounts to " + amount + " pounds");
		window.speechSynthesis.speak(speech); //omilia//

window.speechSynthesis.cancel(); //omilia//

Τροποποίηση στον κώδικα έτσι ώστε όταν κάνουμε κλικ σε κάθε μπάλα να ανοίγει ένα νέο παράθυρο με τα αποτελέσματα της αναζήτησης στο google για τον αντίστοιχο δωρητή στο chart.js

window.open("http://www.google.com/search?q=" +d.donor);});

![2](https://user-images.githubusercontent.com/22959040/39838652-a3b9e4ac-53e2-11e8-8461-0e78ca9adb97.jpg)

Tροποποίηση του κώδικα της εφαρμογής έτσι ώστε το ποντίκι να λειτουργεί και ως μεγεθυντικός φακός όταν μεταφέρεται επάνω από τις λέξεις του κειμένου στο index.html
class=zoom
![3](https://user-images.githubusercontent.com/22959040/39838602-88ad525c-53e2-11e8-94e5-5eaea0363275.jpg)
Δημιουργία μίας ακόμα επιλογής ομαδοποίησης των δεδομένων Split by the amount of the donation στο index.html ,στο  style.css και στο chart.js
![4](https://user-images.githubusercontent.com/22959040/39838537-533052d2-53e2-11e8-8071-c2bc5497f2a1.jpg)

index.html

<li><a href="#" role="button" class="pure-button switch" id="group-by-amount"> <p class=zoom> Split by the amount of the donation </p> </a>
</li>

chart.js
if (name === "group-by-amount"){ 
		sound.play();
		$("#initial-content").fadeOut(250);
		$("#value-scale").fadeOut(250);
		$("#view-donor-type").fadeOut(250);
		$("#view-party-type").fadeOut(250);
		$("#view-source-type").fadeOut(1000);
		$("#view-amount-type").fadeIn(250);
		return amountType();
	}
  
  function amountType() {
	
	force.gravity(0)
		.friction(0.85)
		.charge(function(d) { return -Math.pow(d.radius, 2) / 2.5; })
		.on("tick", amounts)
		.start();
}
function total() {

	force.gravity(0)
		.friction(0.9)
		.charge(function(d) { return -Math.pow(d.radius, 2) / 2.8; })
		.on("tick", all)
		.start();
}
function amounts(e) {
	node.each(moveToAmount(e.alpha));

		node.attr("cx", function(d) { return d.x; })
			.attr("cy", function(d) {return d.y; });
}

function moveToAmount(alpha) {
	return function(d) {
		var centreX;
		var centreY;
		if (d.value <= 500000){
			centreX = svgCentre.x +70;
			centreY = svgCentre.y -70;
		} else if (d.value <= 5000000){
			centreX = svgCentre.x +450;
			centreY = svgCentre.y -70;
		} else if (d.value <= 10000000){
			centreX = svgCentre.x +70;
			centreY = svgCentre.y +250;
		} else {
			centreX = svgCentre.x +500;
			centreY = svgCentre.y +250;
		}
		
		d.x += (centreX - d.x) * (brake + 0.02) * alpha * 1.1;
		d.y += (centreY - d.y) * (brake + 0.02) * alpha * 1.1;
	};
}

style.css

#view-party-type, #view-donor-type, #view-source-type,  #view-amount-type
#view-amount-type {
    height: 100%;
}

#amountofdonation {
    left: 500px;
    top: 150px;
    position: absolute;
}

#Upto500000 {
    left: 200px;
    top: 200px;
    position: absolute;
}

#Upto5000000{
    left: 750px;
    top: 250px;
    position: absolute;
}

#Upto10000000 {
    left: 150px;
    top: 800px;
    position: absolute;
}

#Upto20000000 {
    left: 750px;
    top: 700px;
    position: absolute;
}

Δημιουργία ενός αρχείου .csv στον φάκελο participants του αποθετηρίου του κώδικα.
Με τίτλο τον Α.Μ. και περιεχόμενο τα στοιχεία μου

Τοποθέτηση 5 φωτογραφιών δωρητών στο φάκελο photos
 Στο δεύτερο Παραδοτέο πραγματοποιήθηκε η υλοποίηση του πρώτου ερωτήματος , δηλαδή όταν το ποντίκι εισέρχεται σε έναν από τους κύκλους του γραφήματος, εμφανίζονται οι πληροφορίες του αντίστοιχου δωρητή να εμφανίζεται (και να επεκτείνεται δυναμικά) η σειρά των εικόνων με τους δωρητές πάνω από τους οποίους πέρασε ο δείκτης του ποντικιού  στο γράφημα.Αυτό έγινε με την προσθήκη τροποίηση των index.html , chart.js και style.css
 
 index.html
 <div id = "photos"></div>
 
 chart.js
 
 var pht = document.createElement("IMG", );
	pht.setAttribute("src", imageFile);
	pht.setAttribute("height", "42");
	pht.setAttribute("width", "42");
	document.getElementById("photos").appendChild(pht);
  
  style.css
  
  #photos{
    left:1200px;
    top:130px;
    width:210px;
  position:absolute;
}

Για την υλοποιήση της εργασίας χρησιμοποιήθηκαν ως βοήθεια βίντεο στο youtube και αναζήτηση σε σελίδες στο διαδύκτιο μέσω google . Επιπλέον χρειάστηκαν γνώσεις προγραμματισμού (html , css) . Χρησιμοποιήθηκε το google chrome . Η ζωγραφική για την επεξεργασία των εικόνων καθώς και το photoshop . Επίσης η σελίδα επεξεργάστηκε μέσω github . 
Συμπερασματικά είναι μια εργασία που απαιτεί αρκετή μελέτη και συμβάλει στην εκμάθηση προγραμματισμού ,καθώς και στην εκμάθηση και την καλύτερη διαχείρηση του github.

