Download Link: https://assignmentchef.com/product/solved-hpc-project-33-parallel-programming-using-openmp
<br>






This project will introduce you to parallel programming using OpenMP.

<h1>1.      Parallel reduction operations using OpenMP [10 points]</h1>

The file <em>dotProduct/dotProduct.cpp </em>contains a serial version of a C++ code that computes the dot product <em>α </em>= <em>a<sup>T </sup></em>· <em>b </em>of two vectors <em>a </em>∈ R<em><sup>N </sup></em>and <em>b </em>∈ R<em><sup>N</sup></em>. Below is a code snippet:

<table width="675">

 <tbody>

  <tr>

   <td width="675"><strong>for </strong>(<strong>int </strong>i = 0; i &lt; N; i++) {alpha += a[i] * b[i];} } time_serial = wall_time() – time_start; cout &lt;&lt; “Serial execution time = ” &lt;&lt; time_serial &lt;&lt; ” sec” &lt;&lt; endl;<strong>long double </strong>alpha_parallel = 0; <strong>double </strong>time_red = 0;</td>

  </tr>

 </tbody>

</table>

Solve the following tasks:

<ol>

 <li>Implement a parallel version of the dot product (i) using the OpenMP <em>reduction </em>clause, and (ii) using the OpenMP <em>parallel </em>and <em>critical </em></li>

 <li>Run the serial and both parallel versions on the ICS cluster and measure their execution times. Make a performance scaling chart for the serial version and both parallel versions using various number of threads from <em>p </em>= 1<em>,….,</em>24 for various vector lengths of <em>N </em>= 100<em>,</em>000, <em>N </em>= 1<em>,</em>000<em>,</em>000, <em>N </em>= 10<em>,</em>000<em>,</em>000, <em>N </em>= 100<em>,</em>000<em>,</em>000, and <em>N </em>= 1<em>,</em>000<em>,</em>000<em>,</em>000. In addition to the performance scaling, plot the parallel efficiency for all these dot product benchmarks.</li>

 <li>Please summarize your observations at what size of <em>N </em>it would be beneficial to use a multi-threaded version of a dot product on one compute node of ICS cluster .</li>

</ol>

Hint: Next let’s build the code. You have to load the gcc module.

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="8df8fee8ffcde1e2eae4e3">[email protected]</a>]$ module load gcc

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="b4c1c7d1c6f4d8dbd3ddda">[email protected]</a>]$ make

Execute the code using 1 thread:

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3e4b4d5b4c7e5251595750">[email protected]</a>]$ salloc –exclusive

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="95e0e6f0e7d5fcf6e6fbfaf1f0cdcd">[email protected]</a>]$ export OMP_NUM_THREADS=1

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="0d787e687f4d646e7e636269685555">[email protected]</a>]$ ./dotProduct

or <em>t </em>threads:

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="146167716654787b737d7a">[email protected]</a>]$ salloc –exclusive [<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="5520263027153c36263b3a31300d0d">[email protected]</a>]$ export OMP_NUM_THREADS=t

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="cbbeb8aeb98ba2a8b8a5a4afae9393">[email protected]</a>]$ ./dotProduct

1

<h1>2.      The Mandelbrot set using OpenMP [30 points]</h1>

Write a sequential code in C to visualize the Mandelbrot set. The set bears the name of the “Father of the Fractal Geometry,” Benoˆıt Mandelbrot. The Mandelbrot set is the set of complex numbers <em>c </em>for which the sequence (<em>z,z</em><sup>2 </sup>+ <em>c,</em>(<em>z</em><sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c,</em>((<em>z</em><sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c,</em>(((<em>z</em><sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c</em>)<sup>2 </sup>+ <em>c,…</em>) does not approach infinity. Mandelbrot set images are made by sampling complex numbers and determining for each whether the result tends towards infinity when a particular mathematical operation is iterated on it. Treating the real and imaginary parts of each number as image coordinates, pixels are colored according to how rapidly the sequence diverges, if at all. More precisely, the Mandelbrot set is the set of values of <em>c </em>in the complex plane for which the orbit of 0 under iteration of the complex quadratic polynomial <em>z<sub>n</sub></em><sub>+1 </sub>= <em><sup>z</sup></em><em><sub>n</sub></em><sup>2 </sup>+ <em>c </em>remains bounded. That is, a complex number <em>c </em>is part of the Mandelbrot set if, when starting with <em>z</em><sub>0 </sub>= 0 and applying the iteration repeatedly, the absolute value of <em>z<sub>n </sub></em>remains bounded however large <em>n </em>gets. For example, letting <em>c </em>= 1 gives the sequence 0<em>,</em>1<em>,</em>2<em>,</em>5<em>,</em>26<em>,… </em>which tends to infinity. As this sequence is unbounded, 1 is not an element of the Mandelbrot set. On the other hand, <em>c </em>= −1 gives the sequence 0<em>,</em>−1<em>,</em>0<em>,</em>−1<em>,</em>0<em>,… </em>which is bounded, and so −1 belongs to the Mandelbrot set. The set is defined as follows:

M := {<em>c </em>∈ C : the orbit<em>z,f<sub>c</sub></em>(<em>z</em>)<em>,f<sub>c</sub></em><sup>2</sup>(<em>z</em>)<em>,f<sub>c</sub></em><sup>3</sup>(<em>z</em>)<em>,… </em>stays bounded}

where <em>f<sub>c </sub></em>is a complex function, usually <em>f<sub>c</sub></em>(<em>z</em>) = <em>z</em><sup>2 </sup>+ <em>c </em>with <em>z,c </em>∈ C. One can prove that if for a <em>c </em>once a point of the series <em>z,f<sub>c</sub></em>(<em>z</em>)<em>,f<sub>c</sub></em><sup>2</sup>(<em>z</em>)<em>,… </em>gets farther away from the origin than a distance of 2, the orbit will be unbounded, hence <em>c </em>does not belong to M. Plotting the points whose orbits remain within the disk of radius 2 after MAXITERS iterations gives an approximation of the Mandelbrot set. Usually a color image is obtained by interpreting the number of iterations until the orbit “escapes” as a color value. This is done in the following pseudo code:

<table width="675">

 <tbody>

  <tr>

   <td width="675"><strong>for </strong>all c in a certain range <strong>do</strong>z = 0 n = 0<strong>while </strong>|z| &lt; 2 and n &lt; MAX_ITERS <strong>do </strong>z = zˆ2 + c n = n + 1 end <strong>while </strong>plot n at position c end <strong>for</strong></td>

  </tr>

 </tbody>

</table>

The entire Mandelbrot set in Figure 1 is contained in the rectangle −2<em>.</em>1 ≤ &lt;(<em>c</em>) ≤ 0<em>.</em>7, −1<em>.</em>4 ≤ =(<em>c</em>) ≤ 1<em>.</em>4. To create an image file, use the routines from <em>mandel/pngwriter.c </em>found in the git repository like so:

<strong>#include </strong>“pngwriter.h”

png_data* pPng = png_create (width, height); <em>// create the graphic // plot a point at (x, y) in the color (r, g, b) (0 &lt;= r, g, b &lt; 256) </em>png_plot (pPng, x, y, r, g, b);

png_write (pPng, filename); <em>// write to file</em>

You need to link with -lpng. You can set the RBG color to white (<em>r,g,b</em>) = (255<em>,</em>255<em>,</em>255) if the point at (<em>x,y</em>) belongs to the Mandelbrot set, otherwise it can be (<em>r,g,b</em>) = (0<em>,</em>0<em>,</em>0)

<em>// plot the number of iterations at point (i, j) </em><strong>int </strong>c = ((<strong>long</strong>) n <sub>*</sub> 255) / MAX_ITERS; png_plot (pPng, i, j, c, c, c);

Record the time used to compute the Mandelbrot set. How many iterations could you perform per second? What is the performance in MFlop/s (assume that 1 iteration requires 8 floating point operations)? Try different image sizes. Please use the following C code fragment to report these statistics.

printf (“Total time: %g millisconds
”, (nTimeEnd-nTimeStart)/1000.0);

printf (“Image size: %ld x %ld = %ld Pixels
”, IM_WIDTH, IM_HEIGHT, (IM_WIDTH*IM_HEIGHT)); printf (“Total number of iterations: %ld
”, nTotalIterationsCount);

Figure 1: The Mandelbrot set

printf (“Avg. time per pixel: %g microseconds
”, (nTimeEnd – nTimeStart)/((IM_WIDTH * IM_HEIGHT)); printf (“Avg. time per iteration: %g microseconds
”,(nTimeEnd-nTimeStart)/nTotalIterationsCount); printf (“Iterations/second: %g
”, nTotalIterationsCount/(nTimeEnd-nTimeStart)*1e6); printf (“MFlop/s: %g
”, nTotalIterationsCount * 8.0 / (nTimeEnd-nTimeStart));

Solve the following problems:

<ol>

 <li>Implement the computation kernel of the Mandelbrot set in <em>mandel/mandel seq.c</em>:</li>

</ol>

<table width="639">

 <tbody>

  <tr>

   <td width="639">x = cx; y = cy; x2 = x * x; y2 = y * y;<em>// compute the orbit z, f(z), fˆ2(z), fˆ3(z), …</em><em>// count the iterations until the orbit leaves the circle |z|=2.</em><em>// stop if the number of iterations exceeds the bound MAX_ITERS.</em><em>// TODO</em><em>// &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; CODE IS MISSING</em><em>// &lt;&lt;&lt;&lt;&lt;&lt;&lt;&lt; CODE IS MISSING</em><em>// n indicates if the point belongs to the mandelbrot set // plot the number of iterations at point (i, j) </em><strong>int </strong>c = ((<strong>long</strong>)n * 255) / MAX_ITERS; png_plot(pPng, i, j, c, c, c); cx += fDeltaX;} cy += fDeltaY;} <strong>unsigned long </strong>nTimeEnd = get_time();<em>// print benchmark data</em>printf(“Total time:                                                        %g millisconds
”,(nTimeEnd – nTimeStart) / 1000.0);printf(“Image size:                                                           %ld x %ld = %ld Pixels
”,</td>

  </tr>

 </tbody>

</table>

<ol start="2">

 <li>Count the total number of iterations in order to correctly compute the benchmark statistics. Use the variable nTotalIterationsCount.</li>

 <li>Parallelize the Mandelbrot code that you have written using OpenMP. Compile the program using the GNU C compiler (gcc) with the option -fopenmp. Compare the timings of the parallelized program to those of the sequential program using a meaningful graphical representation.</li>

</ol>

Hint: Next let’s build and execute the code with <em>t </em>threads. You have to load the gcc module.

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="4134322433012d2e26282f">[email protected]</a>]$ module load gcc

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="e693958394a68a89818f88">[email protected]</a>]$ make

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="2055534552604c4f47494e">[email protected]</a>]$ salloc –exclusive

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3144425443715852425f5e55546969">[email protected]</a>]$ export OMP_NUM_THREADS=t

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="84f1f7e1f6c4ede7f7eaebe0e1dcdc">[email protected]</a>]$ ./mandel_omp

<h1>3.      Bug hunt [15 points]</h1>

You can find in the code directory for this project a number of short OpenMP programs (<em>bugs/omp bug1 1-5.c</em>), which all contain compile-time or run-time bugs. Identify the bugs, explain what is the problem and suggest how to fix it (there is no need to submit the correct modified code).

Hints:

<ol>

 <li><em>c: </em>check tid</li>

 <li><em>c: </em>check shared vs. private</li>

 <li><em>c: </em>check barrier</li>

 <li><em>c: </em>stacksize! <a href="https://stackoverflow.com/questions/13264274/why-segmentation-fault-is-happening-in-this-openmp-code">http://stackoverflow.com/questions/13264274</a></li>

 <li><em>c: </em>locking order?</li>

</ol>

<h1>4.      Parallel histogram calculation using OpenMP [15 points]</h1>

The following code fragment calculates a histogram with 16 bins from a random sequence with a normal distribution stored in an array vec:

<table width="675">

 <tbody>

  <tr>

   <td width="675"><strong>for </strong>(<strong>long </strong>i = 0; i &lt; VEC_SIZE; ++i) { dist[vec[i]]++;} time_end = wall_time();<em>// Write results</em></td>

  </tr>

 </tbody>

</table>

Parallelize the histogram computations using OpenMP. You can find the serial C example code in <em>hist/hist seq.c</em>. Report runtimes for the original (serial) code, the 1-thread and the N-thread parallel versions. Does your solution scale? If it does not, make it scale! (It really should!)

Hint: Next let’s build and execute the code with <em>t </em>threads. You have to load the gcc module.

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="99eceafcebd9f5f6fef0f7">[email protected]</a>]$ module load gcc

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="e194928493a18d8e86888f">[email protected]</a>]$ make

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="bacfc9dfc8fad6d5ddd3d4">[email protected]</a>]$ salloc –exclusive

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="0e7b7d6b7c4e676d7d60616a6b5656">[email protected]</a>]$ export OMP_NUM_THREADS=t

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="e095938592a08983938e8f8485b8b8">[email protected]</a>]$ ./hist_omp

<h1>5.      Parallel loop dependencies with OpenMP [15 points]</h1>

Parallelize the loop in the following piece of code <em>recursion/recur seq.c </em>in the repository using OpenMP:

<table width="675">

 <tbody>

  <tr>

   <td width="675"><strong>double </strong>up = 1.00001; <strong>double </strong>Sn = 1.0; <strong>double </strong>opt[N+1]; <strong>int </strong>n; <strong>for </strong>(n=0; n&lt;=N; ++n) { opt[n] = Sn;Sn *= up;}</td>

  </tr>

 </tbody>

</table>

The parallelized code should work independently of the OpenMP schedule pragma that you will use. Please also try to avoid – as far as possible – expensive operations that might harm serial performance. To solve this problem you might want to use the firstprivate and lastprivate OpenMP clauses. The former acts like private with the important difference that the value of the global variable is copied to the privatized instances. The latter has the effect that the listed variables values are copied from the lexically last loop iteration to the global variable when the parallel loop exits. Please report the scaling of your solution.

Next let’s build and execute the code. You have to load the gcc module.

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="cfbabcaabd8fa3a0a8a6a1">[email protected]</a>]$ module load gcc

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="285d5b4d5a6844474f4146">[email protected]</a>]$ make

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="9feaecfaeddff3f0f8f6f1">[email protected]</a>]$ salloc –exclusive

[<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="3045435542705953435e5f54556868">[email protected]</a>]$ ./recur_seq

<ol start="6">

 <li><strong> Task: Quality of the Report [15 Points]</strong></li>

</ol>

Each project will have 100 points (out of which 15 points will be given to the general quality of the written report).

<ul>

 <li></li>

</ul>