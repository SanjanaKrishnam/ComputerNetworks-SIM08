# ComputerNetworks-SIM08

### Adding the feature of Alternative Backoff with ECN(ABE) for TCP in ns-3<br/>
ABE aims to provide a mechanism to deal with congestion notifications which leads to a less aggressive backoff

### Algorithm
```python
if (packet_drop):
  use normal TCP handling
else if (ecn_notification):
  decrease cwnd by a factor of beta

# beta < traditional tcp beta
```
#### Link to the [paper](http://heim.ifi.uio.no/~naeemk/research/ABE/Networking2017ABE.pdf) used as reference
#### Refer to the [wiki](https://github.com/ayush113/ComputerNetworks-SIM08/wiki) for detailed information

## Roadmap: <br/>
* **Step 1.** **`DONE`** Understanding Traditional TCP with congestion control
* **Step 2.** **`DONE`** Understanding TCP with ECN
* **Step 3.** **`DONE`** Understanding ABE
* **Step 4.** **`DONE`** Differentiating between TCP with ECN and ABE
* **Step 5.** **`DONE`** Making state diagrams for TCP with ECN and for ABE
* **Step 6.** **`DONE`** Understanding ns3 code for ECN
* **Step 7.** **`DONE`** Adding the features of ABE to ns3 ECN implementation
* **Step 8.** **`DONE`** Creating a toplogy to test ABE
* **Step 9.** **`DONE`** Using adaptive red tests with ABE on
* **Step 10.** **`DONE`** Comparing the performance of TCP New Reno with ABE and with normal ECN

## Problems: <br/>

* Router not marking packets in dumbell topology created from scratch
* Inconsistency in results obtained with ARED tests
* Non ECT packets even after enabling ECN in RED tests
* Adding AbeMode attribute in incorrect position
* Reducing cwnd by a factor of beta, ns3 uses integer type for result
  can not use real data type values

## Further Work: <br/>

* Testing ABE with different TCP's to determine its efficiency.
* Using different queuing algorithms to see the impact on performance with ABE
* Measuring Latency under different conditions with ABE, to determine optimal beta values.

