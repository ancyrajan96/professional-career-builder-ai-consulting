from dialogflow_v2.gapic.transports import agents_grpc_transport
from dialogflow_v2.proto import agent_pb2
from dialogflow_v2.proto import agent_pb2_grpc
from dialogflow_v2.proto import validation_result_pb2
from google.longrunning import operations_pb2
from google.protobuf import empty_pb2
from google.protobuf import field_mask_pb2
@@ -932,3 +933,80 @@ def restore_agent(
            empty_pb2.Empty,
            metadata_type=struct_pb2.Struct,
        )

    def get_validation_result(
        self,
        parent=None,
        language_code=None,
        retry=google.api_core.gapic_v1.method.DEFAULT,
        timeout=google.api_core.gapic_v1.method.DEFAULT,
        metadata=None,
    ):
        """
        Gets agent validation result. Agent validation is performed during
        training time and is updated automatically when training is completed.
        Example:
            >>> import dialogflow_v2
            >>>
            >>> client = dialogflow_v2.AgentsClient()
            >>>
            >>> response = client.get_validation_result()
        Args:
            parent (str): Required. The project that the agent is associated with. Format:
                ``projects/<Project ID>``.
            language_code (str): Optional. The language for which you want a validation result. If not
                specified, the agent's default language is used. `Many
                languages <https://cloud.google.com/dialogflow/docs/reference/language>`__
                are supported. Note: languages must be enabled in the agent before they
                can be used.
            retry (Optional[google.api_core.retry.Retry]):  A retry object used
                to retry requests. If ``None`` is specified, requests will
                be retried using a default configuration.
            timeout (Optional[float]): The amount of time, in seconds, to wait
                for the request to complete. Note that if ``retry`` is
                specified, the timeout applies to each individual attempt.
            metadata (Optional[Sequence[Tuple[str, str]]]): Additional metadata
                that is provided to the method.
        Returns:
            A :class:`~google.cloud.dialogflow_v2.types.ValidationResult` instance.
        Raises:
            google.api_core.exceptions.GoogleAPICallError: If the request
                    failed for any reason.
            google.api_core.exceptions.RetryError: If the request failed due
                    to a retryable error and retry attempts failed.
            ValueError: If the parameters are invalid.
        """
        # Wrap the transport method to add retry and timeout logic.
        if "get_validation_result" not in self._inner_api_calls:
            self._inner_api_calls[
                "get_validation_result"
            ] = google.api_core.gapic_v1.method.wrap_method(
                self.transport.get_validation_result,
                default_retry=self._method_configs["GetValidationResult"].retry,
                default_timeout=self._method_configs["GetValidationResult"].timeout,
                client_info=self._client_info,
            )

        request = agent_pb2.GetValidationResultRequest(
            parent=parent, language_code=language_code
        )
        if metadata is None:
            metadata = []
        metadata = list(metadata)
        try:
            routing_header = [("parent", parent)]
        except AttributeError:
            pass
        else:
            routing_metadata = google.api_core.gapic_v1.routing_header.to_grpc_metadata(
                routing_header
            )
            metadata.append(routing_metadata)

        return self._inner_api_calls["get_validation_result"](
            request, retry=retry, timeout=timeout, metadata=metadata
        )