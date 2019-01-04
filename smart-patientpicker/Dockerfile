FROM smartonfhir/patient-browser:node
ENV LAUNCHER_PORT="443"
ENV FHIR_VIEWER_PORT="80"
ENV HAPI_PORT_STU3="443"
ENV HAPI_PORT_STU2="443"
RUN mkdir /usr/share/nginx/html/smart-patientpicker && mv /usr/share/nginx/html/config /usr/share/nginx/html/smart-patientpicker && mv /usr/share/nginx/html/examples /usr/share/nginx/html/smart-patientpicker && mv /usr/share/nginx/html/img /usr/share/nginx/html/smart-patientpicker && mv /usr/share/nginx/html/js /usr/share/nginx/html/smart-patientpicker && mv /usr/share/nginx/html/vendor /usr/share/nginx/html/smart-patientpicker
COPY ./conf /usr/share/nginx/html/smart-patientpicker/config
#Generate config files
RUN sh -c "envsubst < /usr/share/nginx/html/smart-patientpicker/config/stu3-local.tpl > /usr/share/nginx/html/smart-patientpicker/config/stu3-local.json5"
#move config files to examples directory
RUN cp -r /usr/share/nginx/html/smart-patientpicker/config /usr/share/nginx/html/smart-patientpicker/examples/config
#move javascript files for the example patient picker
RUN cp -r /usr/share/nginx/html/smart-patientpicker/vendor /usr/share/nginx/html/smart-patientpicker/js/vendor
#run sed on the deployed js files to replace patient POST with GET
RUN sed -i 's/POST/GET/g' /usr/share/nginx/html/smart-patientpicker/js/index.js
RUN sed -i 's/POST/GET/g' /usr/share/nginx/html/smart-patientpicker/js/index.js.*.map
RUN cp /usr/share/nginx/html/index.html /usr/share/nginx/html/smart-patientpicker/index.html
RUN cp /usr/share/nginx/html/50x.html /usr/share/nginx/html/smart-patientpicker/50x.html