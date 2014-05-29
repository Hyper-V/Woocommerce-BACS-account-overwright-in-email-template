Woocommerce-BACS-account-overwright-in-email-template
=====================================================

//Instead:</br>

<?php do_action( 'woocommerce_email_before_order_table', $order, $sent_to_admin, $plain_text ); ?>

//Following in childtheme\woocommerce\emails\customer-processing-order.php:

<h4 style="font-size: 18pt"><?php echo __( 'Unsere Bankverbindung', 'woocommerce' ); ?></h4>

	 <?php	$bacs_accounts = apply_filters( 'woocommerce_bacs_accounts', $bfm_bacs->account_details );

    	if ( ! empty( $bacs_accounts ) ) {
	    	foreach ( $bacs_accounts as $bacs_account ) {
	    		echo '<ul class="order_details bacs_details">' . PHP_EOL;

	    		$bacs_account = (object) $bacs_account;

	    		// BACS account fields shown on the thanks page and in emails
				$account_fields = apply_filters( 'woocommerce_bacs_account_fields', array(
					'account_name'=> array(
						'label' => __( 'Account Name', 'woocommerce' ),
						'value' => $bfw_bacs_account->account_name
					),
          'bank_name'=> array(
						'label' => __( 'Bank Name', 'woocommerce' ),
						'value' => $bfw_bacs_account->bank_name
					),
          'account_number'=> array(
						'label' => __( 'Account Number', 'woocommerce' ),
						'value' => $bacs_account->account_number
					),
					'sort_code'		=> array(
						'label' => __( 'Sort Code', 'woocommerce' ),
						'value' => $bacs_account->sort_code
					),
					'iban'			=> array(
						'label' => __( 'IBAN', 'woocommerce' ),
						'value' => $bacs_account->iban
					),
					'bic'			=> array(
						'label' => __( 'BIC', 'woocommerce' ),
						'value' => $bacs_account->bic
					)
				), $order_id );

	    		foreach ( $bfw_account_fields as $bfw_field_key => $bfw_field ) {
				    if ( ! empty( $bfw_field['value'] ) ) {
				    	echo '<tr>';
              echo '<td class="' . esc_attr( $bfw_field_key ) . '">' . esc_attr( $bfw_field['label'] ) . ': </td>';
              echo '<strong>' . wptexturize( $bfw_field['value'] ) . '</strong></td>';
							echo '<tr>' . PHP_EOL;
				    }
				}

	    		echo '</table>';
	    	}
	    } ?>
