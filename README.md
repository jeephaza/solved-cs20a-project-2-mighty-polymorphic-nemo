Download Link: https://assignmentchef.com/product/solved-cs20a-project-2-mighty-polymorphic-nemo
<br>
To get warmed up lets implement a Fish class with definition given below:

class Fish { public:

Fish(int capacity, std::string name);// Constructor

Fish(const Fish &amp;other);              // Copy Constructor

~Fish();                                   // Destructor

Fish &amp;operator=(const Fish &amp;other);  // Assignment Operator




void remember(char c);  // Remember c        void forget();     // Clears memory by filling in ‘.’  void printMemory() const;// Prints memory

std::string getName();

protected:

const char* getMemory() const;// Returns memory       int getAmount() const;      // Returns amount remembered       int getCapacity() const;    // Returns memory capacity

private:

// TODO: declare any private member variables/functions here




};

This models a creature that is intelligent enough to remember some capacity of characters at a time. But, a Fish might not use up its entire capacity, it might just remember some amount that is less than its capacity. For example a Fish might be able to remember 10 characters, but may only have encountered 2 so far.

Implement Fish’s member functions:

<ul>

 <li>Fish(int capacity, std::string name);</li>

</ul>

Dynamically allocate capacity-many characters to for the Fish’s memory. Initialize its memory with dot(‘.’)s. If capacity is not positive, then set it to 3 by default. Since, this is a brand new fish it uses none of its capacity. Also, save the Fish’s name.

<ul>

 <li>Fish(const Fish &amp;other);</li>

</ul>

Copy constructor for a Fish, when declaring a new Fish we can make it an exact copy of another.

<ul>

 <li>~Fish();</li>

</ul>

Clean up dynamically allocated memory.

<ul>

 <li>Fish &amp;operator=(const Fish &amp;other);</li>

</ul>

Overloaded assignment operator so we can assign one declared fish to be an exact copy of another declared fish.

<ul>

 <li>void remember(char c);</li>

</ul>

Implement remember. Store the character c into the Fish’s memory. If you already have the max capacity characters memorized, then discard the oldest character in memory to open up a free slot. (This is an example of LRU (Least Recently Used) replacement.).  Update the amount of characters remembered appropriately.

<ul>

 <li>void forget();</li>

</ul>

Implement forget, clear memory by filling dot(‘.’)s into memory. This implies that there are no characters remembered.

<ul>

 <li>void printMemory() const;</li>

</ul>

Print to console what is in Fish’s memory.

<ul>

 <li>std::string getName();</li>

</ul>

Gets the Fish’s name.

<ul>

 <li>const char* getMemory() const;</li>

</ul>

Gets the Fish’s memory.

<ul>

 <li>int getAmount() const;</li>

</ul>

Gets the amount of characters remembered.

<ul>

 <li>int getCapacity() const;</li>

</ul>

Gets the Fish’s capacity.

Below is an example using this new Fish class:

int main() {

Fish *nemo = new Fish(3, “nemo”);        nemo-&gt;remember(‘a’);        nemo-&gt;printMemory();// prints “a.. ”

nemo-&gt;remember(‘b’);        nemo-&gt;remember(‘c’);        nemo-&gt;printMemory();// prints “abc”        nemo-&gt;remember(‘d’);        nemo-&gt;printMemory(); // prints “bcd”

Fish *dory = new Fish(*nemo);      dory-&gt;printMemory(); // prints “bcd”

nemo-&gt;forget();        nemo-&gt;printMemory(); // prints “…”

*dory = *nemo;        dory-&gt;printMemory(); // prints “…”

return 0;

}

<strong>Bubbles: </strong>

Let’s create another class based on our Fish class called Yellowtang.  Yellowtang is just like any other fish except in the presence of bubbles Yellowtang gets excited and can’t remember anything other than BUBBLES! Below is Yellowtang’s class definition:

class Yellowtang :public Fish { public:

Yellowtang(int capacity, std::string name); // Constructor

Yellowtang(const Yellowtang &amp;other);        // Copy Constructor

Yellowtang &amp;operator=(const Yellowtang &amp;other); // Assignment Operator




// Overridden functions  virtual void remember(char c);  virtual void printMemory() const;  virtual void forget();

private:

// TODO: declare any private member variables/functions here };

Since, we’re making a Base class out of Fish and we intend on overriding three of Fish’s functions we must make them virtual, and we should also make the destructor virtual as well, because ALWAYS make base class destructor virtual!  Implement Yellowtang’s member functions:

<ul>

 <li>Yellowtang(int capacity, std::string name);</li>

</ul>

Implement Yellowtang’s constructor which must call its Fish constructor and then initializes any member variables.

<ul>

 <li>Yellowtang(const Yellowtang &amp;other);</li>

</ul>

Copy constructor for a Yellowtang, calls Fish’s copy constructor to copy its Fish component and makes copies of any Yellowtang specific member variables.

<ul>

 <li>Yellowtang &amp;operator=(const Yellowtang &amp;other);</li>

</ul>

Implement Yellowtang’s overloaded assignment operator.  Like all assignment operator overloads this should check to see if Yellowtang is being assigned to itself.  Afterwards, like the copy constructor, should just call Fish’s overloaded assignment operator to assign its Fish.  Then copy any Yellowtang specific member variables, then as always return itself.

<ul>

 <li>virtual void remember(char c);</li>

</ul>

Yellowtang remembers things exactly the way any other Fish does, but in addition keeps track if it has seen any bubbles, represented by the character ‘o’.

<ul>

 <li>virtual void printMemory() const;</li>

</ul>

Yellowtang print’s its memory just like any other Fish, except if Yellowtang remembers any bubbles, in that case Yellowtang just prints “BUBBLES!”

<ul>

 <li>virtual void forget();</li>

</ul>

Yellowtang forgets just like Fish, but in addition to clearing its memory it also forgets that it has seen bubbles.

Below is example usage of Yellowtang:

int main() {

Yellowtang *bubbles = new Yellowtang(3, “bubbles”);

bubbles-&gt;remember(‘t’);        bubbles-&gt;printMemory(); // prints “t..”       bubbles-&gt;remember(‘o’);        bubbles-&gt;printMemory(); // prints “BUBBLES!”

bubbles-&gt;remember(‘a’);        bubbles-&gt;remember(‘b’);        bubbles-&gt;printMemory(); // prints “BUBBLES!”        bubbles-&gt;remember(‘c’);        bubbles-&gt;printMemory(); // prints “abc”

return 0;

}

<strong>Obnoxious Memory: </strong>

Butterflyfish is another type of Fish, except has an extended memory in addition to Fish’s memory.  Not only does it store characters in its limited capacity memory, it also has memory that can expand once it reaches its capacity.  Not only that, it remembers how many times it has seen any character.  Similar to Fish’s memory, the number of unique characters Butterflyfish as seen is not necessarily its capacity.   Butterflyfish’s definition is provided below:

class Butterflyfish :public Fish { public:

Butterflyfish(int capacity, std::string name);  // Constructor

Butterflyfish(const Butterflyfish &amp;other);                        // Copy Constructor

Butterflyfish &amp;operator=(const Butterflyfish &amp;other); // Assignment Operator

virtual ~Butterflyfish();                            // Destructor




// Overridden Functions  virtual void remember(char c);  virtual void printMemory() const;

private:

// TODO: declare any private member variables/functions here




};

<ul>

 <li>Butterflyfish(int capacity, std::string name);</li>

</ul>

Implement Butterflyfish’s constructor which must call its Fish constructor and then initializes its own member variables. Butterflyfish’s dynamically allocated extended memory starts of the same size as Fish’s.  Recall that Butterflyfish’s extended memory keeps track of two things: any unique characters encountered and the number of times it has seen them. It starts off not having seen anything.

<ul>

 <li>Butterflyfish(const Butterflyfish &amp;other);</li>

</ul>

Copy constructor for a Butterflyfish, calls Fish’s copy constructor to copy its Fish component and makes copies of any Butterflyfish specific member variables. Pay special mind to any dynamically allocated member variables.

<ul>

 <li>Butterflyfish &amp;operator=(const Butterflyfish &amp;other);</li>

</ul>

Implement Butterflyfish overloaded assignment operator.  Like all assignment operator overloads this should check to see if Butterflyfish is being assigned to itself.  Afterwards, like the copy constructor, should just call Fish’s overloaded assignment operator to assign its Fish.  Then copy any Butterflyfish specific member variables, like the copy constructor pay special mind to any dynamically allocated member variables, then as always return itself.

<ul>

 <li>virtual void remember(char c);</li>

</ul>

Butterflyfish remembers things exactly the way any other Fish does, but in addition keeps of unique characters and a count of each time it has seen those characters.  If its extended memory fills up to its capacity, Butterflyfish expands its character and counter memory by doubling its capacity.  <strong> </strong>

<ul>

 <li>virtual void printMemory() const;</li>

</ul>

Butterflyfish print’s its memory just like any other Fish, but in addition to that it says “I’m Obnoxious!”, then prints out each of the unique characters it has seen along with the number of times it has seen them.

Example usage below:

<table width="503">

 <tbody>

  <tr>

   <td colspan="2" width="371">int main() {</td>

   <td rowspan="2" width="132">…I’m Obnoxious!cadI’m Obnoxious! I’ve seen:    a 3 times   x 1 times   b 1 times   c 1 times   d 1 times…I’m Obnoxious! I’ve seen:    a 3 times   x 1 times   b 1 times   c 1 times   d 1 times</td>

  </tr>

  <tr>

   <td width="48">                }</td>

   <td width="323">Butterflyfish *tad= new Butterflyfish(3, “tad”);tad-&gt;printMemory();      tad-&gt;remember(‘a’); tad-&gt;remember(‘x’); tad-&gt;remember(‘a’); tad-&gt;remember(‘b’); tad-&gt;remember(‘c’); tad-&gt;remember(‘a’); tad-&gt;remember(‘d’); tad-&gt;printMemory();      tad-&gt;forget(); tad-&gt;printMemory(); return 0;</td>

  </tr>

  <tr>

   <td width="48"></td>

   <td width="323"></td>

   <td width="132"></td>

  </tr>

 </tbody>

</table>




<strong>Polyquarium: </strong>

Let’s now create an aquarium to house all our Fish!

const int MAX_FISH = 20;

class Aquarium { public:

<table width="490">

 <tbody>

  <tr>

   <td width="288">      Aquarium();</td>

   <td width="202">// Default Constructor</td>

  </tr>

  <tr>

   <td width="288">      bool addFish(Fish* fish);</td>

   <td width="202">// Add Fish to Aquarium</td>

  </tr>

  <tr>

   <td width="288">      Fish *getFish(int n);</td>

   <td width="202">// Get Fish at nth index</td>

  </tr>

  <tr>

   <td width="288">      void oracle();</td>

   <td width="202">// Read the Fish minds</td>

  </tr>

 </tbody>

</table>

void feed(std::string food); // Put food into Aquarium

<table width="490">

 <tbody>

  <tr>

   <td width="288">      void startle();private:</td>

   <td width="202">// Makes the Fish forget</td>

  </tr>

  <tr>

   <td width="288">      Fish * m_fish[MAX_FISH];</td>

   <td width="202">// Pointers to Fish.</td>

  </tr>

  <tr>

   <td width="288">      int m_nFish;};</td>

   <td width="202">// Number of Fish.</td>

  </tr>

 </tbody>

</table>




<ul>

 <li>Aquarium();</li>

</ul>

Initially there are no Fish in the Aquarium.

<ul>

 <li>bool addFish(Fish* fish);</li>

</ul>

Implement addFish, which takes a pointer to Fish. If the Fish cannot be added because the Aquarium already has MAX_FISH-many Fish residing, return false and don’t add any. Otherwise, return true.

<ul>

 <li>Fish *getFish(int n);</li>

</ul>

Implement getFish, which returns the pointer to the nth Fish that is added. Return nullptr if there is less than n Fish in the Aquarium, or if n is an invalid position.

<ul>

 <li>void oracle();</li>

</ul>

Oracle reads the Fishies’ minds; It prints the memory of all Fish in the Aquarium along with indicating which Fish had those thoughts.

<ul>

 <li>void feed(std::string food);</li>

</ul>

Feed the Fish by providing a string of characters, each Fish in turn will encounter a character and remember that character, once encountered no other Fish can encounter that character.  For example, suppose you have two Fish and if you feed the Fish “abc”, the first Fish will encounter the ‘a’, the second Fish will encounter the ‘b’, finally the first Fish will encounter the ‘c’.

<ul>

 <li>void startle();</li>

</ul>

Startle will cause all the Fish to forget.










Example usage and output:

<table width="593">

 <tbody>

  <tr>

   <td width="425">int main() { Fish *nemo = new Fish(3, “nemo”);  nemo-&gt;remember(‘a’);  nemo-&gt;remember(‘c’); Fish *dory = new Fish(*nemo); Butterflyfish *tad= new Butterflyfish(4, “tad”);  tad-&gt;remember(‘a’);  tad-&gt;remember(‘a’); Yellowtang *bubbles= new Yellowtang(3, “bubbles”);  bubbles-&gt;remember(‘t’);std::cout &lt;&lt; “———-AQUARIUM” &lt;&lt; std::endl;  Aquarium aq;  aq.addFish(nemo);  aq.addFish(dory);  aq.addFish(tad);  aq.addFish(bubbles);  aq.oracle();  std::cout &lt;&lt; “———-Feed” &lt;&lt; std::endl;  aq.feed(“abcdefghijkl”);  aq.oracle();  std::cout &lt;&lt; “———-Bubbles!” &lt;&lt; std::endl;  aq.feed(“oooo”);  aq.oracle();  std::cout &lt;&lt; “———-Boo!” &lt;&lt; std::endl;  aq.startle();  aq.oracle(); delete bubbles;  delete tad;  delete dory;  delete nemo; return 0;}</td>

   <td width="167">———-AQUARIUM nemo ac. nemo ac. tad aa..I’m Obnoxious! I’ve seen:    a 2 times bubbles t.. ———-Feed nemo aei nemo bfj tad acgk I’m Obnoxious! I’ve seen:    a 2 times   c 1 times   g 1 times   k 1 times bubbles dhl ———-Bubbles! nemo eio nemo fjo tad cgko I’m Obnoxious! I’ve seen:    a 2 times   c 1 times   g 1 times   k 1 times   o 1 times bubbles BUBBLES!———-Boo!nemo … nemo … tad ….I’m Obnoxious! I’ve seen:    a 2 times   c 1 times   g 1 times   k 1 times   o 1 times bubbles …</td>

  </tr>

 </tbody>

</table>




fish.h yellowtang.h butterflyfish.h aquarium.h fish.cpp yellowtang.cpp butterflyfish.cpp aquarium.cpp

You will have your own main.cpp for testing, but do not include it with your submission. Combine everything into a zip file name &lt;lastname&gt;_&lt;id&gt;.zip, for example nguyen_123456.zip.  Note that when you resubmit on canvas it will postpend your file name with a number indicating its submission order, this is ok. If I take these 8 files, I must be able to compile them using VS2017 without any errors or warnings. Be sure to you do not introduce any compilation or link errors.


