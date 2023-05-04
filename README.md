Download Link: https://assignmentchef.com/product/solved-csc2001f-assignment-6-graphs
<br>
This assignment concerns using directed graphs to develop a simulation of a very cheap taxi service offered by supermarket chain QnQ. This service is cost-effective for QnQ partly because taxis follow only some limited routes through the city.

<ul>

 <li>Taxis are stationed at QnQ shops.</li>

 <li>Clients are people who ask for a QnQ taxi to take them from a QnQ pickup spot to the nearest QnQ</li>

</ul>

shop.

<ul>

 <li>Edges in the graph represent routes the taxis take, modelled as <strong>a weighted directed graph.</strong></li>

 <li>As the fare for the taxi is a set price, clients are only taken to the nearest QnQ shop.</li>

 <li>To minimise costs, the nearest taxi must go to the client’s pickup spot, and from there it must take the client to the nearest QnQ shop.</li>

</ul>




Part one of the assignment will be automatically marked, while part two will be manually marked.

<strong>Please note that the Automarker will generate random data, so you will not have the same situation every time you run it. </strong>

<h1>Part one: client-trip simulation</h1>

Given an incoming call, the problem is to identify the taxi that can make the lowest cost trip to the client and then to the nearest shop.

You will write a program called ‘SimulatorOne.java’ that accepts as input a file containing data on roads, shop locations and incoming calls. The program will then, for each call, calculate and output details of the (best) shortest trip.

You must use Dijkstra’s algorithm to calculate the lowest cost path from taxi to client to shop.

Input format:

<em>&lt;number of nodes&gt;&lt;newline&gt; </em>

<em>{&lt;source node number&gt; {&lt;destination node number&gt; &lt;weight&gt;}<sup>*</sup>&lt;newline&gt;}<sup>* </sup></em>

<em>&lt;number of shops&gt;&lt;newline&gt; </em>

<em>{&lt;shop node number&gt;}<sup>*</sup>&lt;newline&gt; </em>

<em>&lt;number of clients&gt;&lt;newline&gt; </em>

<em>{&lt;client node number&gt;}<sup>*</sup>&lt;newline&gt; </em>

(‘<em>{x}<sup>*</sup></em>’ mean zero or more of item x.)

The last line is a chronologically ordered series of calls, where each call is represented by the number of the node that the client calls a taxi from.

Example:

5

<ul>

 <li>4 15</li>

 <li>0 14 2 7 3 23</li>

 <li>0 7</li>

 <li>1 23 4 16</li>

 <li>2 15 3 9</li>

</ul>

2

<ul>

 <li>3</li>

</ul>

3

<ul>

 <li>4 2</li>

</ul>

Representing the following weighted di-graph:




Output format:

Output is ordered by call event:




client<em> &lt;node C<sub>0</sub>&gt; </em>

<em>&lt;results for client at node C<sub>0</sub>&gt; </em>

<em>… </em>

client<em> &lt;node C<sub>N</sub>&gt; </em>

<em>&lt;results for client at node C<sub>N</sub>&gt; </em>

<em> </em>

The results for a client (at a given node) consist of details of the lowest cost pick-up (shortest path from a taxi to the client), and then details of the lowest cost drop-off (shortest path from the client to a shop).




taxi <em>&lt;taxi node T<sub>X</sub>&gt; </em>

<em>&lt;shortest path from T<sub>X </sub>to C<sub>n</sub>&gt; shop &lt;shop node S<sub>i</sub>&gt; </em>

<em>&lt;shortest path from C<sub>n</sub> to S<sub>i</sub>&gt; </em>




If there is more than one taxi with the lowest cost pick-up, then these are output in ascending order of taxi node, and if there is more than one shop with the lowest cost drop-off then these are output in ascending order of shop node:




taxi <em>&lt;taxi node T<sub>X</sub>&gt; </em>

<em>&lt;shortest path from T<sub>X</sub> to C<sub>n</sub>&gt; </em>

…

taxi <em>&lt;taxi node T<sub>Y</sub>&gt;  </em>

<em>&lt;shortest path from T<sub>Y</sub> to C<sub>n</sub>&gt; </em>

<em> </em>

<em>… </em>

<em>shop &lt;shop node S<sub>j</sub>&gt; </em>

<em>&lt;shortest path from C<sub>n</sub> to S<sub>j</sub>&gt; </em>

<em> </em>

A path is represented by the sequence of nodes traversed.

In the case that there is more than one minimum-cost trip from a taxi at node <em>T<sub>i</sub></em> to a client at node <em>C<sub>j</sub></em>, the cost of these solutions is reported <strong><em>instead of </em></strong>these paths, i.e. output takes the following form:

…

taxi <em>&lt;taxi node T<sub>X</sub>&gt; </em>multiple solutions cost <em>&lt;</em>C<sub>min</sub><em>&gt;</em>.

…




Similarly, of there is more than one minimum-cost trip from a client at node <em>C<sub>j</sub></em> to a shop at node <em>S<sub>k </sub></em>, output takes the form:

…

<em>shop &lt;shop node S<sub>i</sub>&gt; </em>multiple solutions cost <em>&lt;</em>C<sub>min</sub><em>&gt;</em>.  …

If there is no path from any taxi to a client or from a client to a shop, the output takes this form:

…

client<em> &lt;node C<sub>N</sub>&gt; </em>cannot be helped

…

Example (assuming input data of example on page 2 above):

client 1 taxi 3

3 1 shop 0 multiple solutions cost 14

client 4

taxi 0

0 4

shop 3 4 3

client 2

taxi 0

0 4 2

taxi 3

3 1 2 shop 0

2 0







Results for the client at node 1 (the first call event) are followed with the results for the client at node 4 (the second call event) are followed with the results for the client at node 2 (the third call event).

In the case of the first call event, using a taxi at node 3 and travelling to the shop at node 0 gives the shortest trip. There are in fact two drop-off routes that the taxi can follow (1 0 and 1 2 0).

In the case of the second call event, there is only one shortest path, and this trip is for a taxi at node 0 dropping off at the shop at node 3.

In the case of the third call event, there are two locations from which taxis can be dispatched that give rise to the same pick-up cost, so both these results are given in ascending order of taxi-node number i.e. taxi from node 0 first and then taxi from node 3.

<h1>Part two: extension</h1>

<strong>This part will NOT be marked by the Automarker. </strong>

Create a new version of your simulation called ‘SimulatorTwo.java’ that incorporates some advanced features, such as the following:

<ul>

 <li>Taxis are not always stationed at shops.</li>

 <li>Taxis can take a client to any shop.</li>

 <li>Some/all taxis can carry 2 or more clients.</li>

 <li>The number of taxis is finite.</li>

 <li>Taxis and shops belong to different companies (e.g. QnQ and Shopfite), and taxis only operate between the shops of their own company.</li>

 <li>Client calls are interspersed with traffic reports requiring changes to the graph weightings.</li>

</ul>

These examples are under specified. We want you to exercise your creativity.

Along with your code, you should submit a ‘readme.txt’ document containing a brief description of the features that you have implemented.

<h1>Development requirements</h1>

For part 2 you are required make use of these additional tools:

<ul>

 <li>javadoc, for documentation generation</li>

</ul>

make, for automation of compilation, documentation generation, and cleaning of files