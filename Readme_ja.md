# jitsi-videobridge-zabbix-template
## このZabbixテンプレートについて
このZabbixテンプレートは、WEB会議システムJitsiMeetのコンポーネントである、
VideoBridgeの統計情報を取得・監視するためのものです。

## 利用方法
### 前提
本テンプレートでは、VideoBridgeのColibri REST APIに接続して統計情報を取得します。
VideoBridge側で、REST APIを有効化してください。

## テンプレートの適用
1. ZabbixのWEB UIからテンプレートをインポートしてください
m. インポートされた「Template Jitsi Videobridge」を対象のホスト等に登録してください
3. 監視対象のColibri REST APIの接続先のマクロを変更してください

  + `{$JITSI_COLIBRI_HOST}`: Colibri REST APIの接続先IPアドレス・ホスト(デフォルト:localhost)
  + `{$JITSI_COLIBRI_PORT}`: Colibri REST APIの接続先ポート(デフォルト:8080)

4. デフォルトのデータ取得間隔は1分であるため、1分程度経過するとデータの取得・グラフの作成が行われます。

## 取得する統計情報について
VideoBridgeの統計情報の公式情報は次のURLです。

* https://github.com/jitsi/jitsi-videobridge/blob/master/doc/statistics.md

ただし、この情報はソースコードの更新から遅れているため、取得できる情報が異なる可能性があります。
このテンプレートは、次のJSONをもとに作成されています。

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
  
## 動作試験環境
本テンプレートは次の環境で試験を行いました。

* Docker版Jitsi stable-9779
* Zabbix 7


## 制限事項
* 取得可能な統計情報の仕様により、会議室毎の参加者など細かい情報の取得は行なえません。
  + 取得できるのは、Jitsiシステム全体の統計情報です

* 統計情報は、情報取得時の統計を返却する仕様であるため、過去のデータを登録することはできません。

# 謝辞
このテンプレートは次のプロジェクトで作成されたテンプレートを、株式会社デージーネットがJitsi stable-9779/Zabbix 7に
合わせて修正を行い、VideoBridgeの統計情報の監視に特化させたものです。

* https://github.com/romantico88/jitsi_videobridge_zabbix_stats/

元々のテンプレートとは内容が異なるため、上記プロジェクトへのPRを行わず、
元のプロジェクトと同様のGPLv3ライセンスで公開を行っています。
romantico88とコントリビューターの仕事に多大なる感謝の意を表します。
