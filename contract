#![no_std]
use soroban_sdk::{contract, contracterror, contractimpl, log, Address, String, Env, Symbol};

#[contracterror]
#[derive(Copy, Clone, Debug, Eq, PartialEq, PartialOrd, Ord)]
#[repr(u32)]
pub enum Error {
    NotOwner = 1,
    NoOwner = 2,
}

#[contract]
pub struct SorobanNFTContract;

#[contractimpl]
impl SorobanNFTContract {
    pub fn initialize (env: Env, admin: Address, name: String, symbol: Symbol){
        log!(&env, "admin: {}, name: {}, symbol: {}", admin, name, symbol);
    }

    ///minting a seat token
    pub fn mint(env: Env, owner: Address, seat: u32) -> u32 {
        //check if the seat is already taken
        if env.storage().persistent().has(&seat){
            panic!("this seat is already taken!!!");
        }

        env.storage().persistent().set(&seat, &owner);
        seat
    }

    //check the owner of the seat
    pub fn owner_of (env: Env, seat: u32) -> Option<Address>{
        env.storage().persistent().get(&seat)
    }

    /// Transfer Adddress "from" to Address "to"
    pub fn transfer(env: Env, seat: u32, from: Address, to: Address) -> Result<u32, Error>{
        let current_owner: Option<Address> = env.storage().persistent().get(&seat);
        log!(&env, "check current_owner: {}", current_owner);

        match current_owner {
            Some(current_owner) => log!(&env, ""),
            None => return Err(Error::NotOwner),
        }

        env.storage().persistent().set(&seat, &to);
        Ok(seat)
    }
}
