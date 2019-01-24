var sign = [];

var symbol = function (x,y,size) {
    this.mult = size;
    this.x = x;
    this.y = y;
    this.rot = 0;
    this.rot2 = 0;
    this.rot3 = 220;
    this.sw = 3;
    this.grow = true;
    this.timer = 0;
    this.lap = 150;
    this.shade = 255;
    this.light = true;
    this.delay = 1000; // make it last longer
};

symbol.prototype.draw = function() {
    // each group of shapes have their own pushMatrix
    // and popMatrix grids so that rotation speed do not 
    // over lap. this also makes customization of 
    // rotation speeds much easier to handle
    
    pushMatrix();
    translate(this.x, this.y);
    
    noFill();
    strokeWeight(5);
    stroke(194, 246, 255);
    
    // first inner solid arc and its rotation speed
    rotate(this.rot);
    arc(0, 0, 20*this.mult, 20*this.mult, 0, 310);
    
    popMatrix();
    
    pushMatrix();
    translate(this.x, this.y);
    strokeWeight(5);
    
    // outer solid arc and its rotation speed
    rotate(-this.rot2/2);
    arc(0, 0, 35*this.mult, 35*this.mult, 110, 310);
    
    popMatrix();
    
    pushMatrix();
    translate(this.x, this.y);
    strokeWeight(3);
    
    // solid moving "clock hand" and its rotation speed
    rotate(this.rot3);
    line(0, 11*this.mult, 0, 16.5*this.mult);
    
    popMatrix();
    
    pushMatrix();
    translate(this.x, this.y);
    
    textSize(30);
    fill(255, 255, 255);
    var f = createFont("monospace"); // display of "Loading"
    textFont(f);
    textAlign(CENTER,CENTER);
    text("Loading   ", 0, 0);
    //text(this.shade, 20 ,20);
    //text(this.delay, 95 ,63);
    strokeWeight(6);
    stroke(255, 255, 255);
    // the changing period after "Loading"
    if(this.timer > this.lap*(1/4)) {point(45,8);}
    if(this.timer > this.lap*(1/2)) {point(63,8);}
    if(this.timer > this.lap*(3/4)) {point(81,8);}
    popMatrix();
    
};
symbol.prototype.static = function() {
    
    // inner ring of dashes
    pushMatrix();
    translate(this.x, this.y);
    rotate(-this.rot/2);
    strokeWeight(3);
    stroke(194, 246, 255);
    
    for(var i = 0; i < 18; i ++) {
        rotate(20); // spacing between each dash
        line(-3, 9*this.mult, 3, 9*this.mult);
        line(-3, 10.5*this.mult, 3, 10.5*this.mult);
    }
    popMatrix();
    
    // outer ring of dashes
    pushMatrix();
    translate(this.x, this.y);
    strokeWeight(3);
    rotate(this.rot2/2);
    
    for(var i = 0; i < 20; i ++) {
        rotate(18); // spacing between each dash
        stroke(89, 144, 153);
        line(-3, 19*this.mult, 3, 19*this.mult);
        line(-3, 17*this.mult, 3, 17*this.mult);
    }
    
    popMatrix();
    
    // middile ring of dashes
    pushMatrix();
    translate(this.x, this.y);
    strokeWeight(this.sw); // big and small stroke weight
    stroke(144 +this.sw*16, 196 +this.sw*16, 205 +this.sw*16);
    rotate(this.rot3 + this.rot2*3);
    
    for(var i = 0; i < 18; i ++) {
        rotate(20);
        point(0, 13*this.mult);
    }
    
    popMatrix();
};
symbol.prototype.move = function() {
    // this area is where the rotation speeds are made.
    // the timers, rotations and the faze in/out 
    // accumulators are calculated here.
    // to make certain things fast you increase the 
    // number added and vice versa.
    
    this.rot ++;
    this.rot2 += 0.5;
    this.rot3 --;
    this.rot4 --;
    
    if(this.sw < 3) {this.grow = true;}
    if(this.sw > 10) {this.grow = false;}
    
    if(this.grow) {this.sw += 0.1;}
    else {this.sw -= 0.1;}
    
    // the changing periods on "loading..."
    this.timer ++;
    if (this.timer > this.lap) {this.timer = 0;}
    
    // for the faze in and out
    if (this.shade >= 255) {this.light = 1;}  // activates faze in
    if (this.shade < 0) {this.delay --;} // start delay count down
    if (!this.delay) {this.light = 0;} // delay count down activates faze out
    
    if (this.light) {this.shade --;} // faze in
    if (this.shade < -1) {this.shade = -1;} // hold shade value at -1 during delay countdown
    if (!this.light) { this.shade ++;} // faze out
    
    // screen 
    fill(0, 0, 0, this.shade);
    rect(0, 0, 600, 600);
};

sign[0] = new symbol(300,300,14.0);

draw = function() {
    background(0, 0, 0);
    
    sign[0].draw();
    sign[0].static();
    sign[0].move();
};

