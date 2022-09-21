# ko

<!---
Note: Do NOT edit directly, this file was generated using https://github.com/chainguard-images/readme-generator
-->

[![CI status](https://github.com/chainguard-images/ko/actions/workflows/release.yaml/badge.svg)](https://github.com/chainguard-images/ko/actions/workflows/release.yaml)

This is an image that contains ko, go, and build-base.<br/><br/>This image is designed for use in situations where you would like to use `ko` with codebases that have C dependencies where `cgo` must be used. In these cases, staticly linking against musl instead of glibc results in smaller binaries.

## Get It!

The image is available on `cgr.dev`:

```
docker pull cgr.dev/chainguard/ko:latest
```

## Supported tags

| Tag | Digest | Arch |
| --- | ------ | ---- |
| `0.11.2-r3` `latest` | `sha256:007f047e0e476675ca22bea58ccfd778a5cc0eb9aed061fe8054e3002b9f5a62`<br/>[View entry in Rekor](https://rekor.tlog.dev/?hash=sha256:007f047e0e476675ca22bea58ccfd778a5cc0eb9aed061fe8054e3002b9f5a62) | `386` `amd64` `arm64` `armv6` `armv7` `ppc64le` `s390x` |


## Usage

### Using with CGO

Navigate to the `example/` directory:

```
cd example/
```

Then run:

```
docker run --rm -it \
  -v ${PWD}:/work \
  --workdir=/work \
  -e KO_DOCKER_REPO=example.com \
  -e CGO_ENABLED=1 \
  cgr.dev/chainguard/ko build ./ \
    --push=false \
    --preserve-import-paths
```

This will build the example program, but not push it, due to `--push=false`.

To push, you will need to mount in your Docker config to provide auth by adding:

```
  -v $DOCKER_CONFIG:/docker-config \
  -e DOCKER_CONFIG=/docker-config \
```

If you're using Docker credential helpers, those will need to be made available in the container as well so that `ko` can invoke them.


## Signing

All Chainguard Images are signed using [Sigstore](https://sigstore.dev)!

<details>
<br/>
To verify the image, download <a href="https://github.com/sigstore/cosign">cosign</a> and run:

```
COSIGN_EXPERIMENTAL=1 cosign verify cgr.dev/chainguard/ko:latest | jq
```

Output:
```
Verification for cgr.dev/chainguard/ko:latest --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - Any certificates were verified against the Fulcio roots.
[
  {
    "critical": {
      "identity": {
        "docker-reference": "ghcr.io/chainguard-images/ko"
      },
      "image": {
        "docker-manifest-digest": "sha256:007f047e0e476675ca22bea58ccfd778a5cc0eb9aed061fe8054e3002b9f5a62"
      },
      "type": "cosign container image signature"
    },
    "optional": {
      "1.3.6.1.4.1.57264.1.2": "schedule",
      "1.3.6.1.4.1.57264.1.3": "992aed8ddc07e81ec5faa6086075069ba7c0fb0d",
      "1.3.6.1.4.1.57264.1.4": "Create Release",
      "1.3.6.1.4.1.57264.1.5": "chainguard-images/ko",
      "1.3.6.1.4.1.57264.1.6": "refs/heads/main",
      "Bundle": {
        "SignedEntryTimestamp": "MEUCIHsSIHq5fspDQgexi6/fzyPtt0ff5MIQt6vOCn237i7LAiEAlSNkOn/jAOmlbsFC1JJ2q85fx8khXIyGlryqLLKTaB4=",
        "Payload": {
          "body": "eyJhcGlWZXJzaW9uIjoiMC4wLjEiLCJraW5kIjoiaGFzaGVkcmVrb3JkIiwic3BlYyI6eyJkYXRhIjp7Imhhc2giOnsiYWxnb3JpdGhtIjoic2hhMjU2IiwidmFsdWUiOiIxMWQ1YTI0MzBjYjM2MTU0ZDk1ODg0YTA3YmZlMDdiMWI2YTc5YjhkYmEwNzY2ZjQ2MTJhM2M0MzFlMDNlYjUwIn19LCJzaWduYXR1cmUiOnsiY29udGVudCI6Ik1FUUNJRHRMZDB5bHRabVVkZmlENGgvWDE2RGpyT3BpZUVydFJqdjRaMWR3ZDVqRUFpQjJoZnhSd3pRbjFCSkJTZEhhME8rWWphU3VPdmxhcitHSTVrQUkzRCtZd2c9PSIsInB1YmxpY0tleSI6eyJjb250ZW50IjoiTFMwdExTMUNSVWRKVGlCRFJWSlVTVVpKUTBGVVJTMHRMUzB0Q2sxSlNVUndSRU5EUVhsdFowRjNTVUpCWjBsVlRUbFZWVGt3Y21wb05IZFRWMjFyTDFkWVdrdFVabXBSY2xoemQwTm5XVWxMYjFwSmVtb3dSVUYzVFhjS1RucEZWazFDVFVkQk1WVkZRMmhOVFdNeWJHNWpNMUoyWTIxVmRWcEhWakpOVWpSM1NFRlpSRlpSVVVSRmVGWjZZVmRrZW1SSE9YbGFVekZ3WW01U2JBcGpiVEZzV2tkc2FHUkhWWGRJYUdOT1RXcEpkMDlVU1hoTlJFbDZUVlJCZUZkb1kwNU5ha2wzVDFSSmVFMUVTVEJOVkVGNFYycEJRVTFHYTNkRmQxbElDa3R2V2tsNmFqQkRRVkZaU1V0dldrbDZhakJFUVZGalJGRm5RVVY1TXpsQ00yVk5PVkowU1cxNlFVMU9XbWRDVms1R2NsQndiSGN3ZFhSV1NsQjRja0lLVVRSblExUlZMM1kxWVVwbEswSnliMjloZUd4bFEzZHFVemxIVEdWbWEyaExabFpDVmxSMWJUWmlOVzk1TkNzNVZFdFBRMEZyWjNkblowcEZUVUUwUndwQk1WVmtSSGRGUWk5M1VVVkJkMGxJWjBSQlZFSm5UbFpJVTFWRlJFUkJTMEpuWjNKQ1owVkdRbEZqUkVGNlFXUkNaMDVXU0ZFMFJVWm5VVlZUWldFdkNtRkZhVEJ1U1VscWRTdEpTRkJuTDFOcWNFSlpiVGxOZDBoM1dVUldVakJxUWtKbmQwWnZRVlV6T1ZCd2VqRlphMFZhWWpWeFRtcHdTMFpYYVhocE5Ga0tXa1E0ZDFwQldVUldVakJTUVZGSUwwSkdiM2RYU1ZwWFlVaFNNR05JVFRaTWVUbHVZVmhTYjJSWFNYVlpNamwwVERKT2IxbFhiSFZhTTFab1kyMVJkQXBoVnpGb1dqSldla3d5ZEhaTWVUVnVZVmhTYjJSWFNYWmtNamw1WVRKYWMySXpaSHBNTTBwc1lrZFdhR015VlhWbFYwWjBZa1ZDZVZwWFducE1NbWhzQ2xsWFVucE1NakZvWVZjMGQwOVJXVXRMZDFsQ1FrRkhSSFo2UVVKQlVWRnlZVWhTTUdOSVRUWk1lVGt3WWpKMGJHSnBOV2haTTFKd1lqSTFla3h0WkhBS1pFZG9NVmx1Vm5wYVdFcHFZakkxTUZwWE5UQk1iVTUyWWxSQlYwSm5iM0pDWjBWRlFWbFBMMDFCUlVOQ1FXaDZXVEpvYkZwSVZuTmFWRUV5UW1kdmNncENaMFZGUVZsUEwwMUJSVVJDUTJjMVQxUkthRnBYVVRSYVIxSnFUVVJrYkU5RVJteFplbFp0V1ZkRk1rMUVaekpOUkdNeFRVUlpOVmx0UlROWmVrSnRDbGxxUW10TlFuZEhRMmx6UjBGUlVVSm5OemgzUVZGUlJVUnJUbmxhVjBZd1dsTkNVMXBYZUd4WldFNXNUVU5KUjBOcGMwZEJVVkZDWnpjNGQwRlJWVVVLUmtkT2IxbFhiSFZhTTFab1kyMVJkR0ZYTVdoYU1sWjZUREowZGsxQ01FZERhWE5IUVZGUlFtYzNPSGRCVVZsRlJETktiRnB1VFhaaFIxWm9Xa2hOZGdwaVYwWndZbXBEUW1sbldVdExkMWxDUWtGSVYyVlJTVVZCWjFJNFFraHZRV1ZCUWpKQlFXaG5hM1pCYjFWMk9XOVNaRWhTWVhsbFJXNUZWbTVIUzNkWENsQmpUVFF3YlROdGRrTkpSMDV0T1hsQlFVRkNaekV6YVZrNVZVRkJRVkZFUVVWamQxSlJTV2RWY2tKQk4wOU9jRzFKZFV0RlQwVnBiVmx3TUhCTVUya0tjWGhvZVZsaVpFTm1SV1Z3ZG01VVJIZEpkME5KVVVSNGMzUjFObVI1Y0U1MlNuVm5TaXRLV0c5UlZGbEZielp3VDFocGJFVktTVVUxVUhaSFFXbFVUd3BtYWtGTFFtZG5jV2hyYWs5UVVWRkVRWGRPY0VGRVFtMUJha1ZCYlhkcFZtWkRTVVJ6WTJGdVkzUk9RbnBrT1c1UVQzTTNkUzlwZVhCM1pIcHFUWGR0Q21weWJsSjRZVVpUU21nd1VsRXJaMGwxUm5KVFFXODVhVE5ETUhOQmFrVkJkRFo0Y0ZwdFlsaGhZbEJvWXpoa1pVVm1OREI0UXpFcmIydzBLMHBCY0ZNS2JVaFlkM0F3TDBad2FtMXBlVFpoY3pKcVZWbElORTkzYjB0WmQyUmFhVGtLTFMwdExTMUZUa1FnUTBWU1ZFbEdTVU5CVkVVdExTMHRMUW89In19fX0=",
          "integratedTime": 1663727477,
          "logIndex": 3645931,
          "logID": "c0d23d6ad406973f9559f3ba2d1ca01f84147d8ffc5b8445c224f98b9591801d"
        }
      },
      "Issuer": "https://token.actions.githubusercontent.com",
      "Subject": "https://github.com/chainguard-images/ko/.github/workflows/release.yaml@refs/heads/main",
      "run_attempt": "1",
      "run_id": "3094780091",
      "sha": "992aed8ddc07e81ec5faa6086075069ba7c0fb0d"
    }
  }
]
```

You can verify that the image was built in Github Actions in this repository from the `Issuer` and `Subject` fields.
</details>

## Build

This image is built with [apko](https://github.com/chainguard-dev/apko).

