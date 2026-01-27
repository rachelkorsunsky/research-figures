Changes made to code over the last month:


I initially incorrectly treated resolution as a distribution rather than a mean by directly histogramming the square root of cos(2DPsi). This was corrected by switching to using TProfiles which computed the event-averaged ⟨cos(2ΔΨ)⟩ (lines 96–102 in my code). I also used a function to convert cos(2DPsi) to the resolution via (lines ~276–295). 


I initially attempted to plot resolution versus centrality because the function I created to calculate it gave values that were outside of the bounds (over 100). I created an impact parameter vs counts graph and calculated the centrality from its values. I then hard-coded these values into centrality bins which gave me extremely small values of resolution later that were 3 orders of magnitude too small. 


 I implemented a sorting function to find specific centrality bins for each time I ran the simulation which improved the overall resolution curve, however the ring-by-ring resolution looked nearly flat and single bins with large errors (>1.0).  Because the graph varied so greatly when I changed the centrality code, I switched it to impact parameter instead because it didn’t require me adding another level of error to the code and I would be able to fix the resolution itself first which restored the physical scaling (0 ≤ R ≤ 1). I intend on plotting it with centrality once I’m certain the ring by ring resolution graphs are correctly being plotted.

 
Because it was taking a large amount of time to regenerate events with enough statistics, I decided to change my macro and start using TTree’s instead with my jobs being linked together by a TChain that would save all jobs into one TTree. I ran 21000 events and saved them in a TTree so I could continue analyzing it. After setting the branch address and keeping the same code logic, this change did not alter the graphs.(lines 19-45).


I started creating diagnostic graphs throughout the calculations. I started by adding a delta psi 2 graph with Joey which looked correct. Then I examined it for the ring by ring delta psi graphs and they appeared to be cut off at -Pi/2 and Pi/2 which was a bug in my Wrap 2 Pi function. (lines 309-313). After changing it, the graphs for the ring by ring DPsi calculations all appeared to be correct. Because I assumed that until this step in the analysis, there wasn’t another large bug due to the graphs looking correct, I started testing what was filling the profile before being converted to resolution (cos 2 delta Psi2).


The average before the resolution calculation (the square root 2* delta cosine 2dpsi) appeared to be an incorrect scaled down version of the resolution calculation which meant I needed more diagnostics and to look further behind in my code. It also meant that the error was likely not in the conversion of cosine to resolution.


I went back and started plotting psi 2 positive with psi 2 negative in an attempt to take a step back in the analysis to see whether they still showed correlation ring by ring. The first time I plotted it, I had incorrect bounds on the histogram. This resulted in the plots having a bright spot in the middle and the rest of the graphs being almost completely empty. After copying the bounds from my overall correlation graph, Ring 0 showed correlation but the rest of the rings showed noise. 


I have included a function library I use in another file called EPDGeometry.h italicized at the bottom of the file (lines 290-329)
I plan on writing print statements to examine this more closely and creating more diagnostic graphs.

