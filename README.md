# test
//#include "struct.h"
//
//char *read_interface(void) {
//    char errbuf[PCAP_ERRBUF_SIZE];
////    pcap_if_t *interfaces,*temp;
////    int i=0;
////    if(pcap_findalldevs(&interfaces,errbuf)==-1) {
////        std::cout << "Could not detect default network interface" << std::endl;
////    }
////    printf("\n the interfaces present on the system are:");
////    for(temp=interfaces;temp;temp=temp->next)
////    {
////        printf("\n%d : %s",i++,temp->name);
////
////    }
//    char *interface = "enp2s0f2";
//    return interface;
//}
//
//// int get_iface_ip(char *iface) {
////    int fd;
////    struct ifreq ifr;
////
////    fd = socket(PF_NETLINK, SOCK_DGRAM, NETLINK_ROUTE);
////    ifr.ifr_addr.sa_family = AF_INET;
////    strncpy(ifr.ifr_name, iface, IFNAMSIZ-1);
////    ioctl(fd, SIOCGIFADDR, &ifr);
////    close(fd);
////    printf("%s\n", inet_ntoa(((struct sockaddr_in *)&ifr.ifr_addr)->sin_addr));
////}
//
//int read_nl_sock(int sock, char *buf, int buf_len) {
//    int msg_len = 0;
//    char *pbuf = buf;
//    struct nlmsghdr *nlhdr = (struct nlmsghdr *)pbuf;
//    while (nlhdr->nlmsg_flags & NLM_F_MULTI) {
//        int len = recv(sock, pbuf, buf_len - msg_len, 0);
//        if (nlhdr->nlmsg_type == NLMSG_DONE) {
//            break;
//        } else {
//            msg_len += len;
//            pbuf += len;
//        }
////        if ((nlhdr->nlmsg_flags & NLM_F_MULTI) == 0) {
////            break;
////        }
//    }
//    return msg_len;
//}
//
//int send_nl_req(uint16_t msg_type, uint32_t seq, void *payload, uint32_t payload_len) {
//    //connection between core and user - returns int
//    int sock_fd = socket(PF_NETLINK, SOCK_DGRAM, NETLINK_ROUTE);
//    struct nlmsghdr *nlmsg;
//    nlmsg = static_cast<nlmsghdr *>(malloc(NLMSG_SPACE(payload_len)));
//
//    memset(nlmsg, 0, NLMSG_SPACE(payload_len));
//    memcpy(NLMSG_DATA(nlmsg), payload, payload_len);
//    nlmsg->nlmsg_type = msg_type;                       /* Length of message including header */
//    nlmsg->nlmsg_len = NLMSG_LENGTH(payload_len);       /* Type of message content */
//    nlmsg->nlmsg_flags = NLM_F_DUMP | NLM_F_REQUEST;    /* Additional flags */
//    nlmsg->nlmsg_seq = seq;                             /* Sequence number */
//    nlmsg->nlmsg_pid = getpid();                        /* Sender port ID */
//
//    free(nlmsg);
//    return sock_fd;
//}
//
//// gw and iface[IF_NAMESIZE] MUST be allocated
//int get_gateway(struct in_addr *gw, char *iface) {
//    struct rtmsg request;
//    char buf[8192];
//    struct nlmsghdr *nlhdr;
//    unsigned int nlen;
//    char gaw[32];
//
//    printf("gaw: %s\n", gaw);
//    memset(&request, 0, sizeof(request));
//    int fd = send_nl_req(RTM_GETROUTE, 0, &request, sizeof(request));
//    // Read responses
//    nlen = read_nl_sock(fd, buf, sizeof(buf));
//    // Parse responses
//    nlhdr = (struct nlmsghdr *)buf;
//    while (NLMSG_OK(nlhdr, nlen)) {
//        struct rtattr *rt_attribute;
//        struct rtmsg *rt_msg;
//        int rt_len;
//        int has_gw = 0;
//
//        rt_msg = (struct rtmsg *)NLMSG_DATA(nlhdr);
//
//        rt_attribute = RTM_RTA(rt_msg);
//        rt_len = RTM_PAYLOAD(nlhdr);
//        for ( ; RTA_OK(rt_attribute, rt_len); rt_attribute = RTA_NEXT(rt_attribute, rt_len))
//        {
//            printf("route attribute type: %d\n", rt_attribute->rta_type);
//            /* Get the gateway (Next hop) */
//            if (rt_attribute->rta_type == RTA_GATEWAY)
//            {
//                inet_ntop(AF_INET, RTA_DATA(rt_attribute), gaw, sizeof(gaw));
//                has_gw = 1;
//            }
//        }
//        if (has_gw) {
//            return 0;
//        }
//        nlhdr = NLMSG_NEXT(nlhdr, nlen);
//    }
//}
////
//int main(int argc, char **argv) {
//    (void*)argc;
//    (void *)argv;
//    char *iface = read_interface();
//    struct in_addr gw_ip;
//    memset(&gw_ip, 0, sizeof(struct in_addr));
//    char iface1[IF_NAMESIZE];
//    memset(iface1, 0, IF_NAMESIZE);
//    int gateway = get_gateway(&gw_ip, iface1);
//    std::cout << "Interface is: " << iface << std::endl;
//    std::cout << gateway << std::endl;
//}
