# Why Thermistor

As users of mobile workstations we believe that instead of controlling performance, people expect a control over:

* Surface temperature of the device (with distinction between bottom & keyboard)
* Fan loudness
* Battery usage

and operate at maximum performance with those constraints.

The project is mainly focused on mobile workstations/gaming laptops like Dell XPS, Dell Precision, Lenovo Legion, Asus ROG etc., but is also applicable to any other laptop and tower device.

## Switching Context

During an office day, a typical user of a mobile workstation may switch the way of operating their device between contexts, which implies different preferences. 

**Docked** 
  The device operates as a tower computer, a user may only care about *Fan loudness* to not disturb others (especially in case of very loud fan).
  
**Powered**
  The device is connected to mains power and used directly. User cares about:
  1. Keyboard surface temperature
  2. Fan loudness as above

**Meeting**
  The device lies on the table and is battery powered. The user now cares about **Battery usage** as the main point.
  
**Lap-top**
  The device lies on lap, usually battery powered. Priorities:
  1. Bottom surface temperature
  2. Top surface temperature
  3. Battery usage
  4. Fan loudness


## The current state

Mobile workstations vary a lot in their cooling performance. Nevertheless, producers usually pack and advertise strong CPU and GPU, which cannot be sustainably cooled at their TDP. This often leads to [overthrottling in such devices](https://github.com/erpalma/throttled). For example, Dell XPS 15 9560 from 2017 has Intel i7-7700HQ (45W TDP) and NVIDIA GeForce GTX 1050 Mobile (~50-70W TDP). There is not way for a laptop with so small heat sink to dissipate 100W of heat. On the other hand, in order to support **lap-top** usage, the bottom notebook surface is partially thermically isolated. That forces the built-in PIDs controllers to be very conservative.

## Goal of the project

Thermistor project aims to look at the aforementioned issue from heat dissipation perspective with specific goals to:
  * measure,
  * predict,
  * detect,
  * apply,
  * help improve.

Thermistor should care about power budget, and boosting, throttling, frequencies should be managed by existing embedded controllers.

# TODO

- [ ] Research reliably setting L1/L2 power limits + measuring package power in Intel CPUs (is intel-rapl enough?)
- [ ] Find reliable API to collect and classify current status:
  - [ ] Temperature: knowing temperature at various points in the device: CPU/GPU package, disk, battery, peripherals.
  - [ ] Estimate environment temperature (location? sensors while idle?)
  - [ ] Fan speed
  - [ ] Fan loudness (microphone? notebookcheck reviews?)
  - [ ] CPU state: freqs, active boost, c-states, power consumption
  - [ ] GPU state: same
  - [ ] Embedded Controller throttling reason
  - [ ] Total power draw: from battery, from charger, charger caps (e.g. minimal 65W USB-PD or stock 160W)
- [ ] Research controllability of mobile Nvidia GPUs power limits + measuring current draw.
- [ ] Find API for controlling the fans if possible.
- [ ] Build a simple feedback thermometers for laboratory work.
- [ ] Learn to measure & model heat dissipation + heat capacity in various settings.
  - [ ]  Remove the external sensors from the model.
- [ ] Apply the model to control power limits dynamically.
- [ ] Detect anomalies to warn users when heat dissipation is far from expected.
- [ ] Check the predictability of power-budgeting the battery.
- [ ] Investigate the ways of increasing heat dissipation capacity:
  - [ ] Test the effect of increasing thermal conductance to the bottom surface: vanilla, with external cooling pad, on lap.
  - [ ] Try to build detachable external heat sink for *docked* setup.
  - [ ] Build a gadget that recycles the heat.


# Awesome list of possible backends
- https://github.com/kitsunyan/intel-undervolt C with support for RAPL, configured through /etc file
- https://github.com/georgewhewell/undervolt Python, understands ThrottleStop
- 
