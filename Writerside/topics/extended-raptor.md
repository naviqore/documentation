# Extended RAPTOR

The theoretical RAPTOR algorithm proposed by Delling et al. [REF], while innovative, lacks several practical features
necessary for real-world applications. These missing elements include reverse time routing (i.e., routing backwards from
the arrival time and stop), key query configurations like setting a maximum walking distance between stops, defining
minimum transfer times, and limiting the number of allowable transfers. Additionally, the original implementation does
not account for diverse travel modes (e.g., tram, bus, rail), accessibility options for wheelchairs and bicycles, or the
ability to route across multiple schedules spanning different service days.

In our extended RAPTOR implementation, we have addressed all of these gaps by incorporating these critical features,
enhancing the algorithm’s usability for real-world transit planning.

## Latest Departure

Implementing latest departure routing, which calculates the latest possible departure from a departure stop given a
specified latest arrival time, did not introduce any new algorithmic concepts. However, achieving this in a way that
minimizes code duplication while maintaining readability presented significant challenges. The primary difficulty lay in
adapting the logic for reverse-time routing. In contrast to earliest arrival routing, where the source stop is always
the departure stop and the target stop is the arrival stop, these roles are reversed in latest departure routing. The
source stop becomes the arrival stop, and the target stop is now the departure stop, as routing progresses backward in
time.

This shift required changes to the variable naming conventions in the code. To avoid confusion, we adopted a generalized
terminology where the "source stop" refers to the stop from which the scanning process begins (regardless of the
direction), and the "target stop" refers to the destination of the scan. Additionally, loops that previously scanned for
the earliest possible departure now had to scan for the latest possible arrival, requiring trips to be processed in
reverse—starting from the latest possible trip rather than the earliest.

One of the biggest challenges was handling the conditional logic, which differs between earliest arrival and latest
departure objectives. For earliest arrival, the algorithm marks the earliest arrival at each stop for further scanning,
while for latest departure, the latest departure is marked. Implementing this distinction without duplicating large
portions of code was nontrivial.

To strike a balance between maintainability and readability, we opted for an approach that introduces checks based on
the current routing direction (i.e., earliest arrival vs. latest departure) within the same codebase, despite the added
complexity. This approach was chosen over duplicating the entire algorithm with minor changes for each routing type, as
the latter would have made long-term maintenance significantly more difficult.

## Multiday

Adjustments to trip mask provider.

* Introduce problem that RAPTOR does not know the concept of service days --> outsource by dependency injection
* Introduce TripMaskProvider
* Discuss limitations of checking trip mask before deciding whether to read stop time.
* Introduce updated stop time array --> figure
* Show differences in sequence diagram, maybe isolated class diagram with trip mask provider interface and stop time
  provider
* Discuss limitations on memory consumption trip masks vs stop time arrays for each service day.

## Range Raptor

* worth mentioning here? --> no new novelty, maybe move to RAPTOR implementation and remove "simple"?

## Accessibility and Bike Information

* Introduce the potential of masking trips to also use this for further query configurations travel mode, accessibility,
  bike etc.

## Caching

* To reduce need of recalculating stop time masks for common query configurations.
