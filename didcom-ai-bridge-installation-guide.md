## Run Affinidi DidCom AI Bridge

# Things that we have to keep running;

- Affinidi mediator - cargo run
- Redis docker 
- Ollama
- Affinidi AI bridge 

## Repositories involved

- Affinidi DIDCom AI Bridge: https://github.com/affinidi/didcomm-ai-bridge
- Affinidi Messaging: https://github.com/affinidi/affinidi-messaging
- 

Steps one by one;

- Install git
- Clone DIDCom AI bridge repo
- Clone Affinidi messaging repo
- Install Rust 
- Install Docker
- Create a redis docker ==>  docker run --name=redis-local --publish=6379:6379 --hostname=redis --restart=on-failure --detach redis:latest
- In affinidi messaging directory, run ==> cargo run --bin setup_environment
- Start affinidi messaging mediator inside affinidi-messaging-mediator directory ==> export REDIS_URL=redis://@localhost:6379
- Run affinidi-messaging-mediator directory => Cargo run 
- Make a copy of the file with file name secrets.json inside conf from ==> https://github.com/affinidi/affinidi-messaging/blob/main/affinidi-messaging-mediator/conf/secrets.json-example
- Run cargo run inside didcom-ai-bridge directory 
- If path is not given update it inside cargo.toml in the above directory 
- Update the version in the tool file if necessary, and run cargo run again. 
- When asked, medaitor DID, enter the DID that we got by running the affinidi mediator project.
- Run ollama, whichever model available.
- Provide the host URL for ollama
- If received an authentication error at 127.0.0.1 from didcom ai bridge, but the mediator is running at 0.0.0.0, so go to affinidi medaitor messaging and update the host url
- 



----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
From Affinidi messaging set-up wizard;

Welcome to the Affinidi Messaging setup wizard

✔ Configure local or remote mediator? · Local Mediator Configuration

Configuring local mediator...
  Mediator DID: did:web:localhost%3A7037:mediator:v1:.well-known
✔ Use existing Mediator DID? · yes
  You will need to ensure that the secrets for the Mediator DID are saved as well!!!

✔ Create new JWT authorization secrets? · yes
   JWT Authorization Secret created:  MFECAQEwBQYDK2VwBCIEIGrucKDfp85nSh9I6fVMh3fU6hdCqTXHaB-A3ZhoZ7XfgSEADC29cocpUZ3O7WIk3mkCAAlf71uwcBR0uzi2unKGQG8

✔ Save mediator configuration? · yes
  Line modified: mediator_did = "${MEDIATOR_DID:did://did:web:localhost%3A7037:mediator:v1:.well-known}"
  Line modified: admin_did = "${ADMIN_DID:did://did:peer:2.Vz6Mkf59ucoMMY4Z1jGJi4qBR69RxArUvck3yT4s3p2FfbPQP.EzQ3shm6m8UGTcXpFAvEMjqp9zrHNbwrPtfsKFygjcvHZ7FAc1}"
  Line modified: jwt_authorization_secret = "${JWT_AUTHORIZATION_SECRET:string://MFECAQEwBQYDK2VwBCIEIGrucKDfp85nSh9I6fVMh3fU6hdCqTXHaB-A3ZhoZ7XfgSEADC29cocpUZ3O7WIk3mkCAAlf71uwcBR0uzi2unKGQG8}"
  Mediator configuration file (./affinidi-messaging-mediator/conf/mediator.toml) updated...

? Create local SSL certificates and root authority for testing/develop
✔ Create local SSL certificates and root authority for testing/development? · yes
  SSL certificates etc saved to (./affinidi-messaging-mediator/conf/keys/)

✔ Save profile with name? · local
✔ Save Profile: local? · yes
  Profile added
  Profiles saved...

  Selected Profile: local

? You need some friends to run the examples! Would you like to auto-cr
✔ You need some friends to run the examples! Would you like to auto-create some friends? · yes
  Friend Alice created with DID: did:peer:2.Vz6MkuactUoX35SKr1usKQkFznBBAkTWbHFp1eetge6r8E9Df.EzQ3shNP6GZScxpbaWpNcvqc92Tw1JmJc2mJ3v3XqCttoykufU
  Friend Bob created with DID: did:peer:2.Vz6MkmaTJ6TEfhuWNe5j4Cn35Ks5VrTZP7B8m5HbB34eAYPjW.EzQ3shXXxJyRETGA6JWe3hNSxgtFjquxvmf46xe84uGJ83ibRW
  Friend Charlie created with DID: did:peer:2.Vz6MkrFaut4nTDL8t4bL6VR4376HapVGZvWoZjQn4CgrkyC58.EzQ3shiSEy47kqhGBDxY7XCSW6o8ZMabWmkZRjWyg2rwTfxQ31
  Friend(?) Malorie created with DID: did:peer:2.Vz6MkprSDavjcMBdVZYSXPKhjDvnrmczefXKDbXgnqxfZsHR8.EzQ3shcshkBgWU55x7Rr4VHNnAmt17kYy7a5phQa1Bmsu7FynB
✔ Save friends to profile: local? · yes

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Affinidi Medatior DID info;

 Running `/Users/alvin/Documents/affinidi/affinidi-messaging/target/debug/mediator`
[Loading Affinidi Secure Messaging Mediator configuration]
Config file(conf/mediator.toml)
Switching to tracing subscriber for all logging...
Loading secrets method(file) path(./conf/secrets.json)
2025-02-28T18:20:06.352691Z  INFO affinidi_messaging_mediator::common::config: Configuration settings parsed successfully.
Config {
    log_level: LevelFilter::INFO,
    log_json: false,
    listen_address: "0.0.0.0:7037",
    mediator_did: "did:web:localhost%3A7037:mediator:v1:.well-known",
    mediator_did_hash: "c40ed136d26f36e696af9d27774284cbc1a96367a6581b8130134cc257425215",
    admin_did: "did:peer:2.Vz6Mkf59ucoMMY4Z1jGJi4qBR69RxArUvck3yT4s3p2FfbPQP.EzQ3shm6m8UGTcXpFAvEMjqp9zrHNbwrPtfsKFygjcvHZ7FAc1",
    mediator_did_doc: "Hidden",
    database: DatabaseConfig {
        functions_file: Some(
            "./conf/atm-functions.lua",
        ),
        database_url: "redis://127.0.0.1/",
        database_pool_size: 10,
        database_timeout: 2,
    },
    streaming_enabled?: true,
    streaming_uuid: "Mac-CMWDWVQK2T.local",
    DID Resolver config: ClientConfig {
        service_address: None,
        cache_capacity: 1000,
        cache_ttl: 300,
        network_timeout: 5s,
        network_cache_limit_count: 100,
        max_did_parts: 12,
        max_did_size_in_kb: 1.0,
    },
    api_prefix: "/mediator/v1/",
    security: SecurityConfig {
        mediator_acl_mode: ExplicitDeny,
        global_acl_default: MediatorACLSet {
            access_list_mode: ExplicitDeny,
            access_list_mode_self_change: true,
            did_blocked: false,
            did_local: true,
            send_messages: true,
            send_messages_self_change: true,
            receive_messages: true,
            receive_messages_self_change: true,
            send_forwarded: true,
            send_forwarded_self_change: true,
            receive_forwarded: true,
            receive_forwarded_self_change: true,
            create_invites: true,
            create_invites_self_change: true,
            anon_receive: true,
            anon_receive_self_change: true,
            self_manage_list: true,
            acl: 131067,
        },
        local_direct_delivery_allowed: false,
        mediator_secrets: "(2) secrets loaded",
        use_ssl: false,
        ssl_certificate_file: "conf/keys/end.cert",
        ssl_key_file: "conf/keys/end.key",
        jwt_encoding_key?: "<hidden>",
        jwt_decoding_key?: "<hidden>",
        jwt_access_expiry: 900,
        jwt_refresh_expiry: 86400,
        cors_allow_origin: CorsLayer {
            allow_credentials: No,
            allow_headers: Const(
                Some(
                    "authorization,content-type",
                ),
            ),
            allow_methods: Const(
                Some(
                    "GET,POST,OPTIONS,DELETE,PATCH,PUT",
                ),
            ),
            allow_origin: Const(
                "*",
            ),
            allow_private_network: No,
            expose_headers: Const(
                None,
            ),
            max_age: Exact(
                None,
            ),
            vary: Vary(
                [
                    "origin",
                    "access-control-request-method",
                    "access-control-request-headers",
                ],
            ),
        },
    },
    processors: ProcessorsConfig {
        forwarding: ForwardingConfig {
            enabled: true,
            future_time_limit: 86400,
            external_forwarding: true,
            report_errors: true,
            blocked_forwarding: {
                "http://127.0.0.1:7037/mediator/v1",
                "ws://127.0.0.1:7037/mediator/v1/ws",
                "did:web:localhost%3A7037:mediator:v1:.well-known",
            },
        },
        message_expiry_cleanup: MessageExpiryCleanupConfig {
            enabled: true,
        },
    },
    Limits: LimitsConfig {
        attachments_max_count: 20,
        crypto_operations_per_message: 1000,
        deleted_messages: 100,
        forward_task_queue: 50000,
        http_size: 10485760,
        listed_messages: 100,
        local_max_acl: 1000,
        message_expiry_seconds: 604800,
        message_size: 1048576,
        queued_messages: 100,
        to_keys_per_recipient: 100,
        to_recipients: 100,
        ws_size: 10485760,
        access_list_limit: 1000,
        oob_invite_ttl: 86400,
    },
}


You can now run the mediator locally using the following command:
  cd affinidi-messaging-mediator && cargo run

You can set the environment variable AM_PROFILE to use this profile in the examples.
  export AM_PROFILE=local

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


