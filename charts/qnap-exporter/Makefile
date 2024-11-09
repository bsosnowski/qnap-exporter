template:
		clear & helm template . --name-template qnap-exporter --namespace qnap-monitoring --values values.yaml

install:
		helm install qnap-exporter oci://ghcr.io/bsosnowski/charts/qnap-exporter

upgrade:
		helm upgrade qnap-exporter oci://ghcr.io/bsosnowski/charts/qnap-exporter

delete:
		helm delete qnap-exporter