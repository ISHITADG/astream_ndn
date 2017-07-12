# astream_ndn
Holds the code to run multiple DASH algorithms to be played by Astream media player over NDN
****************************************************************************************************************************
ALL NODES ARE UBUNTU 14.04 WITH 10MBPS LINK BANDWIDTH

SETUP (in order)
ALL SERVER NODES: AStream(only if we need to test Astream Http server for comparison with ndn file downloading), DASHdataset,  ndn-cpp, NFD(ndn-cxx), ndn-tools, PyNDN2(easy_install), ndnfs-port 

ALL CLIENT NODES: Astream(that includes my ndn code in this repo), ndn-cpp,  NFD(ndn-cxx),  ndn-tools,  PyNDN2(easy_install), ndnfs-port

ALL ROUTERS: ndn-cpp,  NFD(ndn-cxx),  ndn-tools,  PyNDN2(easy_install), ndnfs-port(OPTIONAL)

ALL CACHES: --
****************************************************************************************************************************
TEST (file is reachable from server)
AT NDN server: (inside ndnfs-port directory)
For a new trial: sudo umount -f /tmp/ndnfs; mkdir /tmp/dir /tmp/ndnfs;
Nfd-start 
./build/ndnfs -s -f /tmp/dir /tmp/ndnfs
./build/ndnfs-server

AT NDN ROUTER: nothing

AT NDN REMOTE CLIENT: 
Nfd-start
nfdc register /ndn/broadcast/ndnfs udp://server.simpleNDN.ch-geni-net.geni.case.edu
./build/test-client
show /ndn/broadcast/ndnfs/BigBuckBunny_4s_simple_2014_05_09.mpd
NOTE: NDNFS fetch application is faulty. If show command works, your file should be succesfully fetched using the AStream dashndnclient application.
****************************************************************************************************************************
TEST (ndn version of Astream works)
AT NDN REMOTE CLIENT: 
Modify face url to server.simpleNDN.ch-geni-net.geni.case.edu
python dashndnclient.py -m "/ndn/broadcast/ndnfs/BigBuckBunny_4s_simple_2014_05_09.mpd" -p "basic"
****************************************************************************************************************************
