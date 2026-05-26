#!/usr/bin/env node

// SPDX-License-Identifier: AGPL-3.0-or-later

/**    ----------------------------------------------------------------
 *     solidity-compiler.js
 *     ----------------------------------------------------------------
 *     Copyright ©
 *       Pellegrino Prevete
 *         2024, 2025, 2026
 * 
 *     All rights reserved
 *     ----------------------------------------------------------------
 * 
 *     This program is free software: you can redistribute it and/or
 *     modify it under the terms of the GNU General Public License as
 *     published by the Free Software Foundation, either version 3 of
 *     the License, or (at your option) any later version.
 * 
 *     This program is distributed in the hope that it will be useful,
 *     but WITHOUT ANY WARRANTY; without even the implied warranty of
 *     MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 *     GNU General Public License for more details.
 * 
 *     You should have received a copy of the GNU General Public License
 *     along with this program.
 *     If not, see <https://www.gnu.org/licenses/>.
 */

/* LibEVM writable globals */

  /* global
       wallet_name:
         writable */


/* eslint-disable
     no-unused-vars */

const
  _libcrash =
  require(
    'crash-js');
/* global
     _argv_get */
const
_argv_get =
  _libcrash._argv_get;
/* global
     _argv_url_get */
const
_argv_url_get =
  _libcrash._argv_url_get;
/* global
     _cmdline_check */
const
  _cmdline_check =
    _libcrash._cmdline_check;
/* global
     _homedir_get */
const
  _homedir_get =
    _libcrash._homedir_get;
/* global
     _get_date_human */
const
  _get_date_human =
    _libcrash._get_date_human;
/* global
     _msg_info */
const
  _msg_info =
    _libcrash._msg_info;
/* global
     _msg_error */
const
  _msg_error =
    _libcrash._msg_error;
/* global
     _process_exit */
const
_process_exit =
  _libcrash._process_exit;
const
  _evm_wallet_module =
    require(
      "evm-wallet.js");
/* global
     _evm_wallet:
       writable */
_evm_wallet =
  _evm_wallet_module._evm_wallet;
const
  _libevm_module =
    require(
      "libevm");
/* global
     _libevm_cmdline_parse */
const
  _libevm_cmdline_parse =
    _libevm_module._libevm_cmdline_parse;
/* global
     _libevm_global_variables */
const
  _libevm_global_variables =
    _libevm_module._libevm_global_variables;
/* global
     _libevm_url_parse */
const
  _libevm_url_parse =
    _libevm_module._libevm_url_parse;
/* global
     _wallet_overrides_set */
const
  _wallet_overrides_set =
    _libevm_module._wallet_overrides_set;

function
  _global_variables() {
  /* global
       app_name:
         writable */
  app_name =
    "evm-wallet.js";
  /* global
       runtime_environment:
         writable */
  runtime_environment =
    "";
  /* global
       app_opts:
         writable */
  app_opts =
    [];
  /* global
       call_date:
         writable */
  call_date =
    "";
  /* global
       config_dir:
         writable */
  config_dir =
    "";
  /* global
       cache_dir:
         writable */
  cache_dir =
    "";
  /* global
       tasks_parallel:
         writable */
  tasks_parallel =
    "";
  /* global
       target_networks:
         writable */
  target_networks =
    [];
  /* global
       target_command:
         writable */
  target_command =
    "";
  /* global
       target_key:
         writable */
  target_key =
    "";
  /* global
       target_value:
         writable */
  target_value =
    "";
  /* global
       output_type:
         writable */
  output_type =
    "";
  /* global
       currency_type:
         writable */
  currency_type =
    "";
  /* global
       currency_address:
         writable */
  currency_address =
    "";
  /* global
       networks_all:
         writable */
  networks_all =
    "";
  /* global
       rpc_selection:
         writable */
  rpc_selection =
    "";
  /* global
       key_fingerprint:
         writable */
  key_fingerprint =
    "";
  /* global
       explorer_selection:
         writable */
  explorer_selection =
    "";
  /* global
       retries_max:
         writable */
  retries_max =
    "";
  /* global
       call_timeout:
         writable */
  call_timeout =
    "";
  /* global
       measure_unit:
         writable */
  measure_unit =
    "";
  /* global
       balance_lifespan:
         writable */
  balance_lifespan =
    "";
  /* global
       qr_support:
         writable */
  qr_support =
    "";
  /* global
       quiet:
         writable */
  quiet =
    "";
  /* global
       verbose:
         writable */
  verbose =
    "";
}

function
  _tasks_parallel_auto_detect() {
  if ( networks_all == "y" ) {
    tasks_parallel =
      10;
  }
  else if ( networks_all == "n" ) {
    tasks_parallel =
      1;
  }
  else {
    const
      _msg =
        `Invalid value '${tasks_parallel}' ` +
        `for variable '${tasks_parallel}'`;
    _msg_error(
      _msg,
      1);
  }
}

function
  _call_timeout_auto_detect() {
  if ( typeof(
         call_timeout) == "undefined" ||
       call_timeout == "" ) {
    if ( target_command == "get" ) {
      call_timeout =
        "30000";
    }
    else {
      call_timeout =
        "300000";
    }
  }
}

function
  _target_key_auto_detect() {
  if ( typeof(
         target_key) == "undefined" ||
       target_key == "" ) {
    if ( target_command == "get" ) {
      target_key =
        "name";
    }
  }
}

function
  _key_fingerprint_auto_detect() {
  if ( wallet_name != "" ) {
    // TODO:
    //   implement EVM GNUPG in Javascript
    true;
  }
}

function
  _output_type_check() {
  let
    _flag,
    _type;
  _flag =
    "false";
  const
    _output_types = [
      "",
      "name",
      "address",
      "fingerprint"
    ];
  for ( _type of _output_types ) {
    if ( output_type == _type ) {
      _flag =
        "true";
      break;
    }
  }
  if ( _flag == "false" ) {
    const
      _msg =
        `Invalid output type '${output_type}'.`;
    _msg_error(
      _msg,
      1);
  }
}

async function 
  _overrides_set() {
  if ( call_date == "" ) {
    call_date =
      _get_date_human();
  }
  if ( typeof(
         wallet_name) == "undefined" ||
       wallet_name == "" ) {
    wallet_name =
      "default";
  }
  if ( typeof(
         target_command) == "undefined" ||
       target_command == "" ) {
    target_command =
      "get";
  }
  if ( networks_all == "" ) {
    networks_all =
      "n";
  }
  _tasks_parallel_auto_detect();
  _call_timeout_auto_detect();
  if ( config_dir == "" ) {
    const
      _home =
        _homedir_get();
    config_dir =
      `${_home}/.config/evm-wallet`;
  }
  if ( cache_dir == "" ) {
    cache_dir =
      `${_homedir_get()}/.cache/evm-wallet`;
  }
  _target_key_auto_detect();
  if ( balance_lifespan == "" ) {
    balance_lifespan =
      "3600";
  }
  if ( typeof(
         retries_max) == "undefined" ||
       retries_max == "" ) {
    retries_max =
      "2";
  }
  if ( typeof(
         measure_unit) == "undefined" ||
       measure_unit == "" ) {
    measure_unit =
      "ether";
  }
  if ( currency_type == "" ) {
    if ( currency_address == "" ) {
      currency_type =
        "gas";
    }
    else if ( currency_address != "" ) {
      currency_type =
        "erc20";
    }
  }
  if ( rpc_selection == "" ) {
    // TODO:
    //   remove all references to that
    //   monster
    rpc_selection =
      "kirsh";
  }
  if ( explorer_selection == "" ) {
    // TODO:
    //   remove all references to that
    //   humunculus
    explorer_selection =
      "kirsh";
  }
  // TODO:
  //   explorers api keys, optional frankly
  //   since theres the evm-contracts-source-index
  const
    _wallet_set_up =
      await _wallet_overrides_set(
        "evm-wallet",
        wallet_name,
        "y",
        "n");
  if ( target_networks.length < 1 &&
       networks_all == "n" ) {
    target_networks.push(
      100);
  }
  _key_fingerprint_auto_detect();
  _output_type_check();
  // See https://github.com/openpgpjs/openpgpjs/issues/2004
  if ( qr_support == "" ) {
    qr_support =
      "n";
  }
  return true;
}

function
  _config_show() {
  /* LibEVM-defined global variables */
  /* global
       api_key */
  /* global
       wallet_address */
  /* global
       wallet_password */
  /* global
       wallet_path */
  /* global
       wallet_seed */
  let
    _line;
  const
    _text = [
      `${app_name} configuration:`,
      `                  Call date:   ${call_date}`,
      `        Runtime environment:   ${runtime_environment}`,
      `             Target command:   ${target_command}`,
      `                Wallet name:   ${wallet_name}`,
      `                 Target key:   ${target_key}`,
      `               Target value:   ${target_value}`,
      `               All networks:   ${networks_all}`,
      `       RPC selection method:   ${rpc_selection}`,
      ` Explorers selection method:   ${explorer_selection}`,
      `               Measure unit:   ${measure_unit}`,
      `           Balance lifespan:   ${balance_lifespan}`,
      `             Send options:`,
      `              Currency type:   ${currency_type}`,
      `           Currency address:   ${currency_address}`,
      `             List options:`,
      `                Output type:   ${output_type}`,
      `      Credentials options:`,
      `                Wallet path:   ${wallet_path}`,
      `                Wallet seed:   ${wallet_seed}`,
      `                    API Key:   ${api_key}`,
      `             Wallet address:   ${wallet_address}`,
      `            Key fingerprint:   ${key_fingerprint}`,
      `  Quantum resistant ciphers:   ${qr_support}`,
      `          Network options:`,
      `            Maximum retries:   ${retries_max}`,
      `               Call timeout:   ${call_timeout}`,
      `             Parallel tasks:   ${tasks_parallel}`,
      `           LibEVM options:`,
      `             Target network:   ${target_networks[0]}`,
      `      Application options:`,
      `    Configuration directory:   ${config_dir}`,
      `            Cache directory:   ${cache_dir}`,
    ];
  for ( _line of _text ) {
    _msg_info(
      _line);
  }
}

function
  _usage(
    _exit_code) {
  let
    _line;
  const
    _text = [
      "EVM networks wallet",
      "",
      "Usage:",
      "",
      "  evm-wallet.js",
      "    [options]",
      "    <command>",
      "      <command-args>",
      "",
      "  commands:",
      "    get",
      "      <wallet-name>",
      "      <key>",
      "    list",
      "    <filter>",
      "    set",
      "      <wallet-name>",
      "      <key>",
      "      <value>",
      "    send",
      "      <address>",
      "      <amount>",
      "",
      "  keys:",
      "    address",
      "    balance",
      "    name",
      "    seed",
      "",
      "  networks:",
      "    all those supported by",
      "    'evm-chains-info' as",
      "    well as direct RPC addresses",
      "",
      "  options:",
      "",
      "     -R --rpc-selection              RPC selection method.",
      `       <rpc-selection>               Default: '${rpc_selection}`,
      "",
      "     -S --explorer-selection         Network explorer selection method.",
      `       <explorer-selection-method>   Default: '${explorer_selection}'`,
      "",
      "     -r --retries-max                Maximum number of retries before",
      "       <retries-max>                 failure.",
      `                                     Default: '${retries_max}'`,
      "",
      "     -u --measure-unit               Measure unit. It can be",
      "       <measure-unit>                'ether' or 'wei'.",
      `                                     Default: '${measure_unit}'`,
      "",
      "     -l --balance-lifespan           Maximum threshold in seconds",
      "       <balance-lifespan>            from now after which to consider",
      "                                     the balance outdated.",
      `                                     Default: '${balance_lifespan}'`,
      "",
      "     -a --networks-all               Operation valid for all available",
      "                                     networks.",
      `                                     Default: '${networks_all}'`,
      "",
      "     -P --tasks-parallel             Tasks to perform in",
      "       <tasks-parallel>              parallel/concurrently.",
      `                                     Default: '${tasks_parallel}'`,
      "",
      "     -Q --qr-support                 Quantum resistance support.",
      `       <y/n>                         Default: '${qr_support}'`,
      "",
      "  list options:",
      "",
      "     -o --output-type                It can be 'name', 'address',",
      "       <output-type>                 'name', 'fingerprint'.",
      `                                     Default: '${output_type}'`,
      "",
      "  send options:",
      "",
      "     -t --currency-type              Currency type.",
      "       <currency-type>               It can be 'gas or 'erc20'.",
      `                                     Default: '${currency_type}'`,
      "",
      "     -C --currency                   Address of the ERC20 token",
      "       <address>                     on the network, if type is 'erc20'.",
      `                                     Default: '${currency_address}'`,
      "",
      "  credentials options:",
      "",
      "     -w --wallet-path                Wallet file path.",
      `       <wallet-path>                 Default: '${wallet_path}'`,
      "",
      "     -p --wallet-password            Wallet password file.",
      `       <wallet-password>             Default: '${wallet_password}'`,
      "",
      "     -s --wallet-seed                Wallet seed file.",
      `       <wallet-seed>                 Default: '${wallet_seed}'`,
      "",
      "     -k --api-key                    Etherscan-like service key.",
      `       <wallet-seed>                 Default: '${api_key}'`,
      "",
      "  libEVM options:",
      "",
      "     -n --network                    EVM network name. Accepted",
      "       <network>                     are all those supported by",
      "                                     'evm-chains-info' and RPC addresses.",
      "",
      "  application options:",
      "",
      "     -K --config-dir                 Configuration directory.",
      `       <config-dir>                  Default: '${config_dir}'`,
      "",
      "     -W --cache-dir                  Cache directory.",
      `       <cache-dir>                   Default: '${cache_dir}'`,
      "",
      "     -h --help                       This message.",
      "     -v --verbose                    Enable verbose output.",
      "",
    ];
  for ( _line of _text ) {
    console.log(
      _line);
  }
  _process_exit(
    _exit_code);
}

async function 
  _cmdline_parse() {
  let
    _help_display;
  const
    _argv_args = {
      "booleans": [
        "h",
        "help",
        "v",
        "verbose"
      ],
      "string":
        true
    };
  const
    _argv =
      _argv_get(
        _argv_args);
  const
    _options =
      _argv[
        "_"];
  quiet = 
    "y";
  runtime_environment =
    "node";
  if ( _argv["h"] == true ) {
    _help_display =
      true;
  }
  if ( _argv["help"] == true ) {
    _help_display =
      true;
  }
  if ( ( _options.indexOf(
           "--help") > -1 ||
         _options.indexOf(
           "-h") > -1) ) {
    _help_display =
      true;
  }
  if ( _help_display ) {
    quiet =
      "n";
    await _overrides_set();
    _usage(
      0);
  }
  if ( typeof(
       _argv) != "undefined" &&
       0 < _argv[
             "_"].length ) {
    target_command =
      _argv[
        "_"][
          0];
  }
  if ( typeof(
       _argv) != "undefined" &&
       1 < _argv[
             "_"].length ) {
    if ( target_command == "list" ) {
      target_key =
        _argv[
          "_"][
            1];
    }
    else {
      /* eslint-disable-next-line
           no-global-assign */
      wallet_name =
        _argv[
          "_"][
            1];
    }
  }
  if ( typeof(
       _argv) != "undefined" &&
       2 < _argv[
             "_"].length ) {
    if ( target_command == "list" ) {
      true;
    }
    else if ( target_command == "send" ) {
      const _key = _argv._[2];
      target_key =
          _argv[
            "_"][
              2].toString();
    }
    else {
      /* eslint-disable-next-line
           no-global-assign */
      target_key =
        _argv[
          "_"][
            2];
    }
  }
  if ( typeof(
       _argv) != "undefined" &&
       2 < _argv[
             "_"].length ) {
    target_key =
      _argv[
        "_"][
          2];
  }
  if ( typeof(
       _argv) != "undefined" &&
       3 < _argv[
             "_"].length ) {
    target_value =
      _argv[
        "_"][
          3];
  }
  if ( "R" in _argv ) {
    rpc_selection =
      _argv[
        "R"];
  }
  if ( "rpc-selection" in _argv ) {
    rpc_selection =
      _argv[
        "rpc-selection"];
  }
  if ( "S" in _argv ) {
    explorer_selection =
      _argv[
        "S"];
  }
  if ( "explorer-selection" in _argv ) {
    explorer_selection =
      _argv[
        "explorer-selection"];
  }
  if ( "r" in _argv ) {
    retries_max =
      _argv[
        "r"];
  }
  if ( "retries-max" in _argv ) {
    retries_max =
      _argv[
        "retries-max"];
  }
  if ( "u" in _argv ) {
    measure_unit =
      _argv[
        "u"];
  }
  if ( "measure-unit" in _argv ) {
    measure_unit =
      _argv[
        "measure-unit"];
  }
  if ( "l" in _argv ) {
    balance_lifespan =
      _argv[
        "l"];
  }
  if ( "balance-lifespan" in _argv ) {
    balance_lifespan =
      _argv[
        "balance-lifespan"];
  }
  if ( "a" in _argv ) {
    networks_all =
      "y";
  }
  if ( "networks-all" in _argv ) {
    networks_all =
      "y";
  }
  if ( "P" in _argv ) {
    tasks_parallel =
      _argv[
        "P"];
  }
  if ( "tasks-parallel" in _argv ) {
    tasks_parallel =
      _argv[
        "tasks-parallel"];
  }
  if ( "Q" in _argv ) {
    qr_support =
      _argv[
        "Q"];
  }
  if ( "qr-support" in _argv ) {
    qr_support =
      _argv[
        "qr-support"];
  }
  if ( "o" in _argv ) {
    output_type =
      _argv[
        "o"];
  }
  if ( "output-type" in _argv ) {
    output_type =
      _argv[
        "output-type"];
  }
  if ( "t" in _argv ) {
    currency_type =
      _argv[
        "t"];
  }
  if ( "currency-type" in _argv ) {
    currency_type =
      _argv[
        "currency-type"];
  }
  if ( "C" in _argv ) {
    currency_address =
      _argv[
        "C"];
  }
  if ( "currency" in _argv ) {
    currency_address =
      _argv[
        "currency"];
  }
  _libevm_cmdline_parse(
    _argv);
  if ( _argv[
         "v"] ||
       _argv[
         "verbose"]) {
    verbose =
      true;
  }
  if ( verbose ) {
    quiet =
      "n";
  }
}

function
  _url_parse() {
  const
    _argv =
      _argv_url_get();
  runtime_environment =
    "browser";
  wallet_name =
    _argv_url_get(
      "wallet_name")[
        0];
  rpc_selection =
    _argv_url_get(
      "rpc_selection")[
        0];
  explorer_selection =
    _argv_url_get(
      "explorer_selection")[
        0];
  retries_max =
    _argv_url_get(
      "retries_max")[
        0];
  measure_unit =
    _argv_url_get(
      "measure_unit")[
        0];
  balance_lifespan =
    _argv_url_get(
      "balance_lifespan")[
        0];
  networks_all =
    _argv_url_get(
      "networks_all")[
        0];
  tasks_parallel =
    _argv_url_get(
      "tasks_parallel")[
        0];
  qr_support =
    _argv_url_get(
      "qr_support")[
        0];
  output_type =
    _argv_url_get(
      "output_type")[
        0];
  currency_type =
    _argv_url_get(
      "currency_type")[
        0];
  currency_address =
    _argv_url_get(
      "currency_address")[
        0];
  config_dir =
    _argv_url_get(
      "config_dir")[
        0];
  cache_dir =
    _argv_url_get(
      "cache_dir")[
        0];
  _libevm_url_parse();
  quiet =
    _argv_url_get(
      "quiet");
  if ( quiet.length === 0 ) {
    quiet =
      "n";
  }
}

async function
  _main() {
  let
    _msg,
    _result;
  const
    _overrides_set_up =
      await _overrides_set();
  _config_show();
  const
    app_opts = [
      target_command,
      wallet_name,
      wallet_path,
      wallet_password,
      wallet_seed,
      key_fingerprint,
      config_dir,
      cache_dir,
      networks_all,
      rpc_selection,
      api_key,
      retries_max,
      tasks_parallel,
      call_timeout,
      measure_unit,
      balance_lifespan,
      currency_type,
      currency_address,
      output_type,
      target_key,
      target_value,
      target_networks
    ];
  const
    _results =
      await _evm_wallet.apply(
        null,
        app_opts);
  const
    _results_type =
      typeof(
        _results);
  if ( _results_type == "bigint" ) {
    console.log(
      _results.toString());
  }
  else if ( _results_type == "string" ) {
    console.log(
      _results);
  }
  else if ( _results_type == "object" ) {
    for ( _result of _results ) {
      console.log(
        _result);
    }
  }
  else if ( _results_type == "undefined" ) {
    _msg =
      `No results.`;
    _msg_error(
      _msg,
      1);
  }
  else {
    _msg =
      "Error retrieving results for command. " +
      `Type of return: '${_results_type}'.`;
    _msg_error(
      _msg,
      1);
  }
}

_global_variables();
_libevm_global_variables();
if ( _cmdline_check(
       "solidity-compiler.js") == true ||
     _cmdline_check(
       "solidity-compiler") == true ) {
  _cmdline_parse();
}
else {
  _url_parse();
}
_main();
