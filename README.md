[Japanese](Readme_ja.md)

# jitsi-videobridge-zabbix-template
## About this Zabbix Template
This Zabbix template is designed to collect and monitor statistical information from VideoBridge,
a component of the Jitsi Meet web conferencing system.

## Usage Instructions
### Prerequisites
This template collects statistical information by connecting to VideoBridge's Colibri REST API.
Please ensure that the REST API is enabled on the VideoBridge side.

## Applying the Template
1. Import the template through the Zabbix Web UI
2. Register the imported "Template Jitsi Videobridge" to your target host(s)
3. Modify the macros for the Colibri REST API connection target:
  + `{$JITSI_COLIBRI_HOST}`: Colibri REST API connection IP address/hostname (default: localhost)
  + `{$JITSI_COLIBRI_PORT}`: Colibri REST API connection port (default: 8080)
4. The default data collection interval is 1 minute. Data collection and graph creation will begin after approximately one minute.

## About the Collected Statistics
The official documentation for VideoBridge statistics can be found at:
* https://github.com/jitsi/jitsi-videobridge/blob/master/doc/statistics.md

However, please note that this documentation may lag behind source code updates, so the available information might differ.
This template was created based on the following JSON:

```
{
  "average_participant_stress": 0.01,
  "bit_rate_download": 0,
  "bit_rate_upload": 0,
  "conferences": 0,
  "current_timestamp": "2024-10-24 02:47:27.605",
  "drain": false,
  "dtls_failed_endpoints": 0,
  "endpoints": 0,
  "endpoints_disconnected": 0,
  "endpoints_reconnected": 0,
  "endpoints_sending_audio": 0,
  "endpoints_sending_video": 0,
  "endpoints_with_high_outgoing_loss": 0,
  "endpoints_with_spurious_remb": 0,
  "endpoints_with_suspended_sources": 0,
  "graceful_shutdown": false,
  "healthy": true,
  "inactive_conferences": 0,
  "inactive_endpoints": 0,
  "incoming_loss": 0.0,
  "largest_conference": 0,
  "local_active_endpoints": 0,
  "local_endpoints": 0,
  "muc_clients_configured": 1,
  "muc_clients_connected": 1,
  "mucs_configured": 1,
  "mucs_joined": 1,
  "num_eps_no_msg_transport_after_delay": 0,
  "num_eps_oversending": 0,
  "num_relays_no_msg_transport_after_delay": 0,
  "octo_conferences": 0,
  "octo_endpoints": 0,
  "octo_receive_bitrate": 0,
  "octo_receive_packet_rate": 0,
  "octo_send_bitrate": 0,
  "octo_send_packet_rate": 0,
  "outgoing_loss": 0.0,
  "overall_loss": 0.0,
  "p2p_conferences": 0,
  "packet_rate_download": 0,
  "packet_rate_upload": 0,
  "participants": 0,
  "preemptive_kfr_sent": 0,
  "preemptive_kfr_suppressed": 0,
  "receive_only_endpoints": 0,
  "rtt_aggregate": 0.0,
  "shutting_down": false,
  "stress_level": 0.0,
  "threads": 41,
  "total_bytes_received": 5301841,
  "total_bytes_received_octo": 0,
  "total_bytes_sent": 9586670,
  "total_bytes_sent_octo": 0,
  "total_colibri_web_socket_messages_received": 0,
  "total_colibri_web_socket_messages_sent": 0,
  "total_conference_seconds": 952,
  "total_conferences_completed": 1,
  "total_conferences_created": 1,
  "total_data_channel_messages_received": 209,
  "total_data_channel_messages_sent": 257,
  "total_dominant_speaker_changes": 1,
  "total_ice_failed": 0,
  "total_ice_succeeded": 3,
  "total_ice_succeeded_relayed": 0,
  "total_keyframes_received": 11,
  "total_layering_changes_received": 4,
  "total_packets_received": 35688,
  "total_packets_received_octo": 0,
  "total_packets_sent": 55609,
  "total_packets_sent_octo": 0,
  "total_participants": 3,
  "total_relays": 0,
  "total_video_stream_milliseconds_received": 225691,
  "total_visitors": 0,
  "version": "2.3.168-g28674f78",
  "visitors": 0
}
```

## Test Environment
This template has been tested in the following environment:
* Docker Jitsi stable-9779
* Zabbix 7

## Limitations
* Due to the specifications of available statistics, detailed information such as participants per conference room cannot be collected.
  + Only system-wide statistics for the entire Jitsi system are available
* Due to the specification that statistics return data only for the time of collection, historical data cannot be registered.

# Acknowledgments
This template is a modified version of the template created in the following project, adapted for Jitsi stable-9779/Zabbix 7 
and specialized for monitoring VideoBridge statistics:
* https://github.com/romantico88/jitsi_videobridge_zabbix_stats/

Since the content differs from the original template, instead of submitting a PR to the above project,
it is being released under the same GPLv3 license as the original project.
We express our sincere gratitude to romantico88 and the contributors for their work.

