# csi_packet_content_exp_txt
csi包内容的英文&中文解释

timestamp_low is the low 32 bits of the NIC's 1 MHz clock. It wraps about every 4300 seconds, or 72 minutes. This field was not yet recorded in the sample trace, so all values are arbitrary and always equal 4.
bfee_count is simply a count of the total number of beamforming measurements that have been recorded by the driver and sent to userspace. The netlink channel between the kernel and userspace is lossy, so these can be used to detect measurements that were dropped in this pipe.
Nrx represents the number of antennas used to receive the packet by this NIC, and Ntx represents the number of space/time streams transmitted. In this case, the sender sent a single-stream packet and the receiver used all 3 antennas to receive it.
rssi_a, rssi_b, and rssi_c correspond to RSSI measured by the receiving NIC at the input to each antenna port. This measurement is made during the packet preamble. This value is in dB relative to an internal reference; to get the received signal strength in dBm we must combine it with the Automatic Gain Control (AGC) setting (agc) in dB and also subtract off a magic constant. This process is explained below.
perm tells us how the NIC permuted the signals from the 3 receive antennas into the 3 RF chains that process the measurements. The sample value of [3 2 1] implies that Antenna C was sent to RF Chain A, Antenna B to Chain B, and Antenna A to Chain C. This operation is performed by an antenna selection module in the NIC and generally corresponds to ordering the antennas in decreasing order of RSSI.
rate is the rate at which the packet was sent, in the same format as the rate_n_flags defined above. Note that the antenna bits are omitted, as there is no way for the receiver to know which transmit antennas were used.
csi is the CSI itself, normalized to an internal reference. It is a Ntx×Nrx×30 3-D matrix where the third dimension is across 30 subcarriers in the OFDM channel. For a 20 MHz-wide channel, these correspond to about half the OFDM subcarriers, and for a 40 MHz-wide channel, this is about one in every 4 subcarriers. Which subcarriers were measured is defined by the IEEE 802.11n-2009 standard (in Table 7-25f on page 50).

timestamp_low  是NIC的1 MHz时钟的低32位。它每隔4300秒或72分钟包裹一次。此字段尚未记录在样本跟踪中，因此所有值都是任意值且始终相等4。
bfee_count  只是驱动程序记录并发送到用户空间的波束成形测量总数的计数。所述网络链路内核和用户空间之间的信道是有损耗的，所以这些可用于检测了在该管下降的测量。
Nrx  表示该NIC用于接收数据包的天线数， Ntx表示传输的空间/时间流的数量。在这种情况下，发送方发送单流数据包，接收方使用所有3个天线接收它。
rssi_a， rssi_b和 rssi_c  对应于由每个天线端口的输入处的接收NIC测量的RSSI。该测量在分组前导码期间进行。该值以 dB为单位，相对于内部参考值; 为了获得以 dBm为单位的接收信号强度，我们必须将其与自动增益控制（AGC）设置（ agc）以 dB为单位进行组合，并减去魔术常数。该过程解释如下。
perm  告诉我们NIC如何将来自3个接收天线的信号置换为处理测量的3个RF链。样本值 [3 2 1]意味着天线C被发送到RF链A，天线B被发送到链B，天线A被发送到链C.该操作由NIC中的天线选择模块执行并且通常对应于排序天线按RSSI的降序排列。
rate  是所述数据包被发送，在相同的格式的速率 rate_n_flags定义如上。注意，省略了天线比特，因为接收器无法知道使用了哪些发射天线。
csi  是CSI本身，归一化为内部参考。它是 Ntx × Nrx ×30 3-D矩阵，其中第三维跨越OFDM信道中的30个子载波。对于20MHz宽的信道，这些对应于大约一半的OFDM子载波，而对于40MHz宽的信道，这大约是每4个子载波中的一个。测量了哪些子载波由 IEEE 802.11n-2009标准定义（第50页的表7-25f）。
